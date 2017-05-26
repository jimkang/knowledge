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

GitHub API
----

# How to get all of your GitHub repo names:

    {
      user(login: "jimkang") {
        repositories(first: 100, after: "Y3Vyc29yOjg0NDUzNDg2") {
          nodes {
            name
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
