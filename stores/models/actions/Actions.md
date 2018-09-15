# Actions

Actions are applied on an API for the specific environment

- Generic actions can be reused in layout and instances
- Named layout actions can extend generic actions
- Instances can use layout actions

```js
const actions = {
  generic: {},
  layouts: {},
  instances: {}
};
```

Generic config

```js
const generic = createActions({
  kind: 'generic'
  named: {
    Item,
    Collection
  }
});
```

## Action functions

By default, each action simply delegates directly to the api.

```js
 $update: {
   api: 'update',
 }
```

actions methods will be generated for the particular context:

```js
type IUpdateArgs = {
  id: string,
  type: string
}

// generator function
function update *(args: IUpdateArgs)
  return yield this.api.update(args);
```

## Generic Collection actions

- `add({ type, item })` Add an item (`item`) to the collection
- `remove({ type, id?, item? })` Remove an item from the collection
- `fetch({ type, filter })` Fetch items passing filter from the collection

Generic collection actions delegate to API methods of same name by default

```js
export const Collection = {
  type: 'collection',
  actions: {
    api: ["add", "remove", "fetch"];
  }
}
```

## Generic Item actions

- `update({type, id, item})`
- `delete({type, id, item})`
- `get({type, id, item, name})` get named property (can be a child collection) of item

Generic item actions delegate to API methods of same name by default

```js
export const Item = {
  type: 'collection',
  actions: {
    api: ["update", "destroy", "get"];
  }
}
```

## Action layouts

You can store different configurations of actions and then compose them as needed into
the application action configuration for each environment.

```js
export const layout = createActions({
  kind: "layout",
  named: {
    Person: {
      extends: "Item", // generic.Item
      actions: {
        add(item: Person) {
          return this.$add({ type: "user", item: user });
        }
      }
    }
  }
});
```

## Action configuration composition

Composition of action configuration for `test` environment using action layouts from test and dev.

```js
export const test = {
  ...actions.test.layouts,
  Product: actions.dev.layouts.Product
};
```
