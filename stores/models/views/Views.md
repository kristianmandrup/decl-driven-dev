# Model Views

Model Views are used to add computed properties such as aggregations, virtual props etc. to the model sent to display.

```js
const views = {
  generic: {},
  layouts: {},
  instances: {}
};
```

## Generic view methods

Generic view methods can be reused across models

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

## View layouts

Just like actions you can have multiple variants of named views that can then be composed as needed in the application views

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
