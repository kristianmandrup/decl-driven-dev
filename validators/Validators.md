# Validators

We use JSON schema to validation model

## JSON schema to Yup Validation

- [yup](<[Yup](https://github.com/jquense/yup)>)
- [json-schema-to-yup](https://www.npmjs.com/package/json-schema-to-yup)

### Validation rules

The form generator uses [json-schema-to-yup](https://www.npmjs.com/package/json-schema-to-yup) to generate a Yup validation schema `validation.schema` based on an extended JSON schema definition passed in as a POJO.

```js
  personSchema: {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "$id": "http://example.com/person.schema.json",
    "title": "Person",
    "description": "A person",
    "type": "object",
    "properties": {
      "name": {
        "description": "Name of the person",
        "type": "string"
      },
      "age": {
        "description": "Age of person",
        "type": "number",
        "exclusiveMinimum": 0,
        "required": true
      }
    },
    "required": ["name"]
  }
  // ...
};
```

## Ajx

- [ajv](https://github.com/epoberezkin/ajv#some-packages-using-ajv)

Ajv is f.ex used in [React form controlled](https://github.com/seeden/react-form-controlled)

## Alternative React validations

- [validify](https://github.com/navjobs/validify)

## Model validation

We should use the same validation model used for the form when mutating a store model via the API.

## Middleware

Always use middleware for validation!
