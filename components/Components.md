# Components

Map components to locical names to be used by reference in the declarations

```js
const components = {
  generic: {},
  named: {}
};
```

## Generic

```js
import { SimpleRating } from 'simple-rating'

components.generic = createComponents({
  kind: 'generic'
  environment: "dev",
}, {
  // ...
  rating: {
    component: SimpleRating.component,
    // defaults
    props: {
      exposed: SimpleRating.props,
      defaults: {
        size: 'small'
      }
    }
  }
  // ...
}
```

## Named

```js
components.named = createComponents({
  kind: 'named'
  environment: "dev",
}, {
  // ...
  product: {
    list: {
      rating: {
        extends: 'rating',
        props: {
          size: 'medium'
        }
      },
    card: {
      rating: {
        extends: 'rating',
        props: {
          size: 'small'
        }
      },
    }
    // ...
  }
```
