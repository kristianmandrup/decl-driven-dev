# GraphQL store

In memory GraphQL server

## JSON GraphQL server

The JSON GraphQL server can be used to auto-generate a full in-memory GraphQL server.

```js
module.exports = {
  posts: [
    { id: 1, title: "Lorem Ipsum", views: 254, user_id: 123 },
    { id: 2, title: "Sic Dolor amet", views: 65, user_id: 456 }
  ],
  users: [{ id: 123, name: "John Doe" }, { id: 456, name: "Jane Doe" }],
  comments: [
    {
      id: 987,
      post_id: 1,
      body: "Consectetur adipiscing elit",
      date: new Date("2017-07-03")
    },
    {
      id: 995,
      post_id: 1,
      body: "Nam molestie pellentesque dui",
      date: new Date("2017-08-17")
    }
  ]
};
```

### GraphQL Types

Generated `Post` type from JSON data

```js
type Post {
    id: ID!
    title: String!
    views: Int!
    user_id: ID!
    User: User
    Comments: [Comment]
}
```

Posts query example

```js
{
  Post(id: 1) {
      id
      title
      views
      User {
          name
      }
      Comments {
          date
          body
      }
  }
}
```

### Queries and Mutations

Generated from JSON data

```js
type Query {
  Post(id: ID!): Post
  allPosts(page: Int, perPage: Int, sortField: String, sortOrder: String, filter: PostFilter): [Post]
  _allPostsMeta(page: Int, perPage: Int, sortField: String, sortOrder: String, filter: PostFilter): ListMetadata
}
```

### Entity Mutations

- `create`
- `update`
- `remove`

```js
type Mutation {
  createPost(data: String): Post
  updatePost(data: String): Post
  removePost(id: ID!): Boolean
}
```

### Entity Filter

For each child collection, on item count

- `[collection]_lt` less than <
- `[collection]_lte` less than or equal <=
- `[collection]_gt` greater than >
- `[collection]_gte` greater than or equal >=

```js
type PostFilter {
    q: String
    id: ID
    title: String
    views: Int
    views_lt: Int
    views_lte: Int
    views_gt: Int
    views_gte: Int
    user_id: ID
}
```

The count used in filter?

```js
type ListMetadata {
    count: Int!
}
```

### Scalars

Special types

```js
scalar Date
```

### JSON schema to GraphQL schema

- [graphql-apollo-json-to-schema](https://www.npmjs.com/package/graphql-apollo-json-to-schema)
- [graphql-schema-from-json](https://github.com/marmelab/graphql-schema-from-json)

### GraphQL schema to JSON schema

- [graphql-json-schema](https://www.npmjs.com/package/graphql-json-schema)
