# Item display

## Layouts

- list
- grid

## Styling and Theming

A layout can be provided a styler (which components to use) and a theme via providers.

## Property display

```js
const display.product = {
  // component mappings
  components: [
    title: Title,
    price: Price,
    // ...
  ],
  // map properties to component props
  mapping: {
    title: {
      label: {
        prop: 'name'
        transform: 'capitalize'
      }
    },
    price: 'price',
    image: {
      // prop mappings
      url: 'imageUrl',
      caption: 'name',
      border: true
    }
  },
  layout: {
    title: {
      first: true,
    },
    image: {
      after: 'title',
    },
    price: {
      after: 'image'
    },
    disclaimer: {
      last: true
    }
  }
}
```

## Children display

Use views of

## Actions
