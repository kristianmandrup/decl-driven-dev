# Entity property display

```js
const components.generic = {
  buttons: {
    edit: {
      icon: 'pencil',
      action: 'edit'
    },
    delete: {
      icon: 'trash',
      action: 'delete'
    }
  }
}
```

```js
const display.product = {
  // component mappings
  components: [
    title: Title,
    price: Price,
    // ...
  ],
  // map properties to component props
  mappings: {
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
  controls: {
    layout: {
      display: 'row',
      components: [
        'delete',
        'edit',
      ]
    }
  },
  layout: {
    display: 'stack',
    components: {
      // relative positioning using first, last, after and before
      title: {
        first: true,
      },
      image: {
        after: 'title',
      },
      price: {
        after: 'image'
      },
      actions: {
        before: 'disclaimer'
      }
      disclaimer: {
        last: true
      }
    }
  }
}
```

## Children display

Use views of

## Actions
