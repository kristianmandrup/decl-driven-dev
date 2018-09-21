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

## JSON to JavaScript serializer

- [serializr](https://github.com/mobxjs/serializr)

## Mongoose

- [mongoose-schema-jsonschema](https://www.npmjs.com/package/mongoose-schema-jsonschema)
- [json-schema-to-mongoose](https://github.com/jon49/json-schema-to-mongoose)

## TypeORM

- [Entity configuration via JSON Schema](https://github.com/typeorm/typeorm/issues/1818)

```js
entitySchemas: [
  Object.assign({ target: Post }, require(__dirname + "/Schemas/Post.json"))
];
```
