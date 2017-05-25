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
