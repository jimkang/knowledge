GraphQL
------

- Built around hierarchical queries.
- "Mutations" is the term for updating specific parts of the object tree.
- Server-oriented, rather than peer-to-peer.
  - Updates to a graph from a client can be incremental.
  - For a client to stay in sync, though, it is necessary to query the entire graph, it seems.
  - Does not seem great for syncing from a client copy of a store to a server copy.
- [You can run it on an Express server.](http://graphql.org/graphql-js/running-an-express-graphql-server/)
- GitHub API v4 uses it.
- You can define named queries like this:

      query getNextPageOfCommits($repoName: String!, $lastCursor: String) {
        viewer {
          repository(name: $repoName) {
            defaultBranchRef {
              id
              repository {
                name
              }
              target {
                ... on Commit {
                  id
                  history(first: 100, after: $lastCursor) {
                    pageInfo {
                      hasNextPage
                      endCursor
                    }
                    edges {
                      node {
                        message
                        committedDate
                      }
                    }
                  }
                }
              }
            }
          }
        }
      }
    
   But how do you call that more than once in a single request?

GitHub API
----

# How to get all of your GitHub repo names:

    {
      user(login: "jimkang") {
        repositories(first: 100, after: "Y3Vyc29yOjg0NDUzNDg2") {
          nodes {
            name
            id
            description
          },
          pageInfo {
            endCursor
            hasNextPage
            hasPreviousPage
            startCursor
          }
        }
      }
    }

Then, while `hasNextPage` is true:

    {
      user(login: "jimkang") {
        repositories(first: 100, after: "<endCursor from previous query>") {
          nodes {
            name
            id
            description
          },
          pageInfo {
            endCursor
            hasNextPage
            hasPreviousPage
            startCursor
          }
        }
      }
    }

Paging
-----

Paging is fairly simple if you want to get all of a top-level object that's available. You just get the `endCursor` in one query, then use that in the `after` in the next query.

However, if you want to get all of a top-level object and all of the things in a collection within those objects, it doesn't like it's possible to do conveniently right now. I think you have to first page through all of the top level objects then save an identifier for each that'll let you get the subobject collection in a future series of queries which page through that collection.

e.g. with the GitHub API, if you want all of the repositories for a user and all of the commits in all of the repositories, you first need to do a series of requests that page through all of the repositories and save the default branch ref associated with each repository, then go back and do another series of requests for each repository which page through all of the commits for each branch ref that you saved.

If a user has 300 repos and you can get 100 in a page, that's 3 requests for the repos. Then, for each repo (300 times), you need to do 1+ request to get all the commits.

Unless! You can do some massive `OR` query that gets commit history for commits that match one of 300 different branch refs.

Looks like you cannot do `OR` in query arguments, but you can do multiple queries in a single request. So, after you save all of the repository names, you can build a query like this that has all of the repository names in it:

    {
      viewer {
        a1: repository(name: "godtributes") {
          defaultBranchRef {
            id
            repository {
              name
            }
            target {
              ... on Commit {
                id
                history(first: 100, after: "1bf4c7a1eef4b594404aa831d477e28a24ed7ea1 399") {
                  ...CommitHistoryFields
                }
              }
            }
          }
        }
        a2: repository(name: "off-brand-vine") {
          defaultBranchRef {
            id
            repository {
              name
            }
            target {
              ... on Commit {
                id
                history(first: 100) {
                  ...CommitHistoryFields
                }
              }
            }
          }
        }    
      }
    }

    fragment CommitHistoryFields on CommitHistoryConnection {
      pageInfo {
        hasNextPage
        endCursor
      }
      edges {
        node {
          message
          committedDate
        }
      }
    }

And you would build and run those until you had no more next pages.

Would be nice if more of it could be DRYed up, but right now [fragments cannot be parameterized](https://github.com/facebook/graphql/issues/204).

Turns out a query like the one above (with 300 repos) both asks for too many things at a time for the API and also exceeds the complexity ratings. Even if you cut it down to 50 at a time, you get an error like:

    body {
      "data": null,
      "errors": [
        {
          "message": "The history field and its children is requesting up to 490,000 possible nodes which exceeds the maximum limit of 11,250.",
          "locations": [
            {
              "line": 12,
              "column": 13
            }
          ]
        },
        {
          "message": "Query has complexity of 751, which exceeds max complexity of 215"
        }
      ]
    }

This happens for 17 repos out of 300+. It's probably because those repos have complex histories involving multiple parents.

If you reduce the number of commits to get via `history` to 20, you no longer get the too-many-nodes complaint. 

??: Does the number of queries in one request somehow affect the complexity rating?

