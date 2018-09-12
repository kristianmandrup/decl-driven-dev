# Item display

## Contexts

- collection cell
- individual

## Styling and Theming

A layout can be provided a styler (which components to use) and a theme via providers.

### Example entity display

```js
import { collection, item } from "./product";

export const products = {
  // implicit if entity key present
  type: "entity",
  // entity type, entity is the product (type)
  entity: "product",
  collection, // configs for how to display collections of product
  item // configs for how to display a single product item
};
```

#### Product item

```js
export const item = {
  name: "product",
  entity: "product",
  item: {
    edit: {
      // ...
    }
  }
};
```

#### User item

```js
import { user } from './user'

export const item = {
    name: 'user',
    contexts: {
      login: {
        social: {
          display: user.social,
          route: 'login/social'
        },
        // username + password
        classic: {
          display: user.classic,
          route: 'login/classic'
        }
      },
      edit: {
        profile: user.profile,
        route: 'profile/:id/edit'
      },
      create: {
        registration: {
          display: user.registration,
          route: 'registration'
        }
      }
    }
  },
```
