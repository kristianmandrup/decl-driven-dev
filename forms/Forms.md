# Forms

## Form builder

- [react-final-form](https://github.com/final-form/react-final-form)
- [mobx-form-factory](https://github.com/kristianmandrup/mobx-form-factory)

## Building from declarations

### Form model

- `validation.schema`
- `form.schema`

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

Usage: `model.validation.schema = personSchema`

```js
name: {
  description: 'Name of the person',
  type: 'string'
  maxLength: 20,
  minLength: 3,
},
```

The form will render fields for all properties specified in the validation schema by default, extracting and using whatever field information is provided, falling back to generic field render rules.

## Form schema

The form generator can also take a form schema that specifies exactly which fields to render and which registered field generator to use for each field.

You can register (or override) field generators on the form model as needed.

```js
const fields = {}
fields.generic =
  'alpha-numeric': {
    // ...
  }
}

fields.name = {
  name: {
    extends: 'alpha-numeric',
    length: 20, // default
    chars: 20 // default
  },
  "number:year:future" {
    extends: 'number:year',
    min: () => Year.current()
}


const formLayout = {
  small: {
    maxLength: 20
    maxChars: 20
  },
  medium: {
    minLength: 20,
    maxLength: 40
  },
  large: {
    minLength: 40,
    maxLength: 80
  }
}
```

```js
const personForm = {
  fields: {
    password: {
      input: "password",
      minLength: 8,
      strength: 'strong'
    },
    repeatPassword: {
      input: "password",
      display: ({values, fields}) => {
        return values.password.length > 1
      },
      enable: ({values, fields}) => {
        return values.password.length > fields.password.minLength
      }
    }
    firstName: {
      input: "name",
      placeholder: "First name",
      // ie. state reducer for controlled form value
      transform: (value) => value.capitalize()
      length: 20, // default
      chars: 20 // default
    },
    lastName: {
      input: "name",
      // use named transform
      transform: 'capitalize'
      // derive from humanized field name
      // placeholder: "Last name"
    },
    month: {
      input: "number:month",
      placeholder: "MM"
      // implicit
      // chars: 2
    },
    slash: {
      text: "/"
    },
    year: {
      input: "number:year:future",
      placeholder: "YY",
      // min: derived
      default: ({value, field}) => field.min + 1,
      max: ({value, field}) => field.min + 10,
      // implicit
      // chars: 2
    },
    code: {
      input: "secret",
      chars: 3
    },
    number: {
      input: "number:creditcard"
      // implicit
      // placeholder: "Creditcard number"
      // length: 20,
      // chars: 16
    }
  },
  actions: {
    cancel: {
      enable: ({form}) => {
        return form.dirty
      }
    },
    submit: {
      enable: ({form}) => {
        return form.valid
      }
    }
  }
  layout: {
    align: 'justify left',
    fields: [
      {
        // on medium or larger display, will displayed on one row
        // see formLayout above
        // implicit justify left alignment
        name: ["firstName", "lastName"]
      },
      {
        expiry: [
          {
            year: {
              align: 'left',
              cells: ["month", "slash", "years"],
            }, {
            code: {
              align: 'right',
              cels: ["code"]
            }
          }
      },
      "number"
    ],
    actions: [
      'cancel', 'submit'
    ]

};
```

We should allow (multi?) extension of form declarations.

```js
const developerForm = {
  extends: "personForm",
  fields: {
    languages: {
      input: "select"
    }
  }
};
```

Usage: `model.form.schema = personForm`

## Nested properties and forms

There should be a way to display nested forms for child properties that are non-primitieves, ie. objects or arrays.
