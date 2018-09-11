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
actions.generic = createComponents({
  kind: 'generic'
  environment: "dev",
}, {
  // ...
  rating: {
    component: SimpleRating,
    // defaults
    props: {
      size: 'small'
    }
  }
  // ...
}
```

## Named

```js
actions.generic = createComponents({
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
