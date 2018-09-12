# Entity display

An entity display must have:

- `name` indicating the name of the entity
- `collection` set of displays configs for the entity collection (list, table etc.)
- `item` set of displays configs for a single entity

An entity display may have multiple variants to accomodate different user scenarios.
A `product` could f.ex include a view :

- for display in a list (primary attributes)
- for display in a table (primary attributes)
- to data entry in a form
- for full details display

## Product

- entity display (view of a single entity item or collection)
- aggregate display (view of multiple entities aggregated)

```js
import { main } from "./main";
import { entity } from './entity'
const products = {
  // no name needed when entity property provided, name will be entity name
  entity: "product",
  // provide all the contextual views/displays of the entity
  contexts: {
    // named contexts
    aggregate: {
      // aggregate views etc
      // when displayed in main view such as products "page"
      main
    }
    entity,
};
```

### Entity

```js
import { collection } from "./collection";
import { item } from "./item";
export const entity = {
  // ensures we don't mistakenly assign it to a entity display parent config of wrong type
  entity: "product",
  collection, // special
  item // for single
};
```

See [Entity](./entity/Entity.md) for more
