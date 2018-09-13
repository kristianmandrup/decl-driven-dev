# Stores

A number of stores can be supported through a simple adapter for each

- Redux
- MobX
- Immer
- Unstated
- ...

## Store properties

- [models](./models/Models.md)
- [middleware](./models/Models.md) (optional)
- [transport](./transports/Transports.md) (optional)

Note: middleware and transport can be configured individually for each model if needed.
This means that you can sync models with different backends or APIs, f.ex some using in-memory backing while others connect to a server backend/api etc.

## Redux

- model (implicit)
- actions
- reducers
- selectors (views)
- middleware

## MobX

- model
- actions
- views
- middleware

## MobX State Tree

- model (with types and validation)
- actions
- views
- middleware

Note: You can adapt a MobX state tree to Redux as well.

### JSON schema to MobX

Use [jsonschema-to-mobx-state-tree](https://www.npmjs.com/package/jsonschema-to-mobx-state-tree) to transform a JSON schema to a MobX State Tree model.

## JSON data to MobX

See:

- [json-mobx](https://github.com/danielearwicker/json-mobx)
- [mobx for data](https://danielearwicker.github.io/json_mobx_Like_React_but_for_Data_Part_2.html)

### Immer

- [immer](https://github.com/mweststrate/immer)

### Unstated

- [unstated](https://github.com/jamiebuilds/unstated)
