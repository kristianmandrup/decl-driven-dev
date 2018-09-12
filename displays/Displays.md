# Displays

Displays can be configured as a map of:

- `name` -> display config

```js
const displays = {
  dashboard: {
    // display config for dashboard
  },
  contact: {
    // display config for dashboard
  }
};
```

Best practice is to keep each display config in a separate file

```js
import { dashboard } from "./dashboard";
import { products } from "./products";

export const displays = {
  dashboard,
  products,
  user
  // ...
};
```

## Display types

- single entity display (view of a single entity item or collection)
- multi entity display (view of multiple entities aggregated)
- non-entity display (no entity data displayed)
- display (any display not covered by one of the above)

### Main

```js
const main = {
  name: "main",
  layout: "stack",
  items: ["recommended", "browseAll"]
};
```

```js
const main = {
  name: 'main',
  layout: 'flex',
  items: {
    recommended: {
      first: true
      display: 'recommended'
    },
    browseAll: {
      after: 'browseAll'
    }
  }
}
```

### Alternative config

```js
const main = {
  name: "main",
  layout: "panel2",
  items: {
    primary: recommended,
    secondary: browseAll
  }
};
```

```js
const panel2 = {
  name: "panel2",
  layout: "stack",
  items: [
    (recommended: {
      first: true
      // display: 'recommended'
    }),
    (browseAll: {
      after: "recommended"
      // implicit by convention
      // display: 'browseAll'
    })
  ]
};
```

The following will use the `filtered-collection` layout with slots `filter` and `collection` being provided named displays.

```js
{
  name: 'browseAll',
  layout: 'filtered-collection',
  items: {
    filter: 'textual',
    collection: 'products'
  }
}
```
