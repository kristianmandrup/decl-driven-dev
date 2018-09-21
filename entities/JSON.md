# Stores

## Data

See [json-to-json-schema](https://github.com/mohsen1/json-to-json-schema) for transforming JSON to JSON schema.

Use [json-to-mobx-state-tree](https://transform.now.sh/json-to-mobx-state-tree/) to transform a JSON data structure to MobX State Tree model (first transforms JSON to JSON Schema)

## Fake Data

[json-schema-faker](https://github.com/json-schema-faker/json-schema-faker/)

```js
var schema = {
    type: "object",
    properties: {
      name: {
        type: "string",
        faker: "name.findName"
      },
      email: {
        type: "string",
        format: "email",
        faker: "internet.email"
      }
    },
    required: ["name", "email"]
  }
};

jsf.resolve(schema).then(function(sample) {
  console.log(sample);
  // "[object Object]"

  console.log(sample.name);
  // "John Doe"
});
```

## JSON data to Schemas

Convert JSON Objects to MySQL Table Schema, JSON Schema, Mongoose Schema, ClickHouse Schema, Google BigQuery, or a Generic template for documentation, code generation, and more.

[generate-schema](https://github.com/Nijikokun/generate-schema)

## Schema to Yup Validation

- [json-schema-to-yup](https://www.npmjs.com/package/json-schema-to-yup)

## Schema to TypeScript

- [json-schema-to-typescript](https://github.com/bcherny/json-schema-to-typescript)
- [@gql2ts/from-schema](https://www.npmjs.com/package/@gql2ts/from-schema) generate a namespace for a GraphQL Schema with all possible interfaces/types included.

## JSON to JavaScript serializer

- [serializr](https://github.com/mobxjs/serializr)

## Elastic search

- [es-mapping-to-schema](https://www.npmjs.com/package/es-mapping-to-schema)
- [json-schema-to-es-mapping](https://github.com/kristianmandrup/json-schema-to-es-mapping)

## Mongoose

- [mongoose-schema-jsonschema](https://www.npmjs.com/package/mongoose-schema-jsonschema)
- [json-schema-to-mongoose](https://github.com/kristianmandrup/convert-json-schema-to-mongoose)
- ... many alternatives

## TypeORM

- [Entity configuration via JSON Schema](https://github.com/typeorm/typeorm/issues/1818)

```js
entitySchemas: [
  Object.assign({ target: Post }, require(__dirname + "/Schemas/Post.json"))
];
```

## Schema to GraphQL types

- [jsonschema-to-graphql](https://www.npmjs.com/package/jsonschema-to-graphql)
- [json-schema-to-graphql-types](https://www.npmjs.com/package/json-schema-to-graphql-types)
- []()

## Forms

[Build React forms based on GraphQL API](https://medium.com/@wittydeveloper/build-react-forms-based-on-graphql-apis-7e3acb1f91d7)

- [react-apollo-form](https://github.com/wittydeveloper/react-apollo-form)
- [react-jsonschema-form](https://github.com/mozilla-services/react-jsonschema-form/)
- [Getting started: build a GraphQL Form in 5 minutes](https://github.com/wittydeveloper/react-apollo-form/wiki/Getting-started:-build-a-GraphQL-Form-in-5-minutes)
