# Actions

Actions are applied on an API for the specific environment

- Generic actions can be reused in layout and instances
- Named layout actions can extend generic actions
- Instances can use layout actions

We avoid allows layouts to extend other named layouts as there could well be circular dependencies (TODO: future).

```js
const actions = {
  generic: {},
  layouts: {},
  instances: {}
};
```

## Generic actions

```js
actions.generic = createcreateActions({
  kind: 'generic'
  environment: "dev",
}, {
  Item: {
    actions: {
      // note: Tip, use currying to get rid of type param
      $update({ type, item }) {
        this.api.update({ type, obj });
      },
      $read({ type, id }) {
        this.api.read({ type, obj });
      }
    }
  },
  Collection: {
    actions: {
      $add({ type, item }) {
        this.api.add({ type, obj });
      },
      $find(id) {
        this.api.find({ type, id });
      }
    }
  }
});
```

## Layout actions

```js
actions.dev.layout = createActions({
  kind: 'layout'
  environment: "dev",
}, {
    Person: {
      extends: actions.generic.Item,
      actions: {
        add(user: User) {
          this.$add({ type: "user", obj: user });
        }
      }
    }
  });
```

## Instantiation

```js
actions.test.instances = {
  ...actions.test.layouts.,
  Product: actions.dev.layouts.Product
};
```
