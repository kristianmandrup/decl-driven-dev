# Stores

- Redux
- MobX
- Immer
- GraphQL
- Unstated
- Watermelon
- ...

## MobX

### JSON schema to MobX

Use [jsonschema-to-mobx-state-tree](https://www.npmjs.com/package/jsonschema-to-mobx-state-tree) to transform a JSON schema to a MobX State Tree model.

## JSON data to MobX

See:

- [json-mobx](https://github.com/danielearwicker/json-mobx)
- [mobx for data](https://danielearwicker.github.io/json_mobx_Like_React_but_for_Data_Part_2.html)

## GraphQL

## JSON GraphQL server

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

GraphQL Types

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

```js
type Query {
  Post(id: ID!): Post
  allPosts(page: Int, perPage: Int, sortField: String, sortOrder: String, filter: PostFilter): [Post]
  _allPostsMeta(page: Int, perPage: Int, sortField: String, sortOrder: String, filter: PostFilter): ListMetadata
}
type Mutation {
  createPost(data: String): Post
  updatePost(data: String): Post
  removePost(id: ID!): Boolean
}
type Post {
    id: ID!
    title: String!
    views: Int!
    user_id: ID!
    User: User
    Comments: [Comment]
}
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
type ListMetadata {
    count: Int!
}
scalar Date
```

### JSON schema to GraphQL schema

- [graphql-apollo-json-to-schema](https://www.npmjs.com/package/graphql-apollo-json-to-schema)
- [graphql-schema-from-json](https://github.com/marmelab/graphql-schema-from-json)

### GraphQL schema to JSON schema

- [graphql-json-schema](https://www.npmjs.com/package/graphql-json-schema)

### Immer

- [immer](https://github.com/mweststrate/immer)

### Unstated

- [unstated](https://github.com/jamiebuilds/unstated)
