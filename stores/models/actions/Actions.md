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

Use currying to get rid of type param

Note: By default, each action simply delegates directly to the api

```js
$update({ type, item }) {
  this.api.update({ type, item });
},
```

Example

```js
actions.generic = createActions({
  kind: 'generic'
  environment: "dev",
}, {
  Item: {
    actions: {
      // note: Tip, use currying to get rid of type param
      $update({ type, item }) {
        this.api.update({ type, item });
      },
      $destroy({ type, item }) {
        this.api.destroy({ type, item });
      },
      $get({ type, id }) {
        this.api.get({ type, item });
      }
    }
  },
  Collection: {
    actions: {
      $add({ type, item }) {
        this.api.add({ type, item });
      },
      $remove({ type, item }) {
        this.api.remove({ type, item });
      },
      $find(id) {
        this.api.find({ type, id });
      }
    }
  }
});
```

## Action layouts

You can store different configurations of actions and then compose them as needed into
the application action configuration for each environment.

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

## Action configuration composition

```js
actions.test.instances = {
  ...actions.test.layouts.,
  Product: actions.dev.layouts.Product
};
```
