# Views

```js
const views = {
  generic: {},
  layouts: {},
  instances: {}
};
```

## Generic views

```js
views.generic = {
  List: {
    // requires a default child collection
    $count() {
      this.items ? this.items.length : 0;
    }
  }
};
```

## Layouts

```js
const views.layouts = {
  Person: {
    $extends: ["$List"],
    defaults: {
      childCollection: 'children'
    },
    numberOfChildren: {
      filter: {
        target: 'items',
        compare: {
          prop: 'age',
          type: '<',
          value: 18
        },
        result: 'length'
      },

      // (res) => res.length
    },
    olderThan(age) {
      props: ['age'],
      filter: {
        target: 'items',
        compare: {
          prop: 'age',
          type: '>',
          // ({props, target}) => target.age > props.age
        }
      },
      result: 'length'
      // (res) => res.length
    }
  }
};
```
