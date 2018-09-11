# Adapters

Each adapter must implement

## Collection

### Mutations

- add (update)
- remove

### Queries

- list
  - pagination
  - filter
  - embed

## Item

- delete
- update
- collection

### Special updates

- toggle
- increment
- decrement

```js
const api.adapters = {
  list: adapters.memory.list(),
  map: adapters.memory.map(),
  graphql: adapters.memory.graphQL()
}
```

## Adapter environment mapping

Map API environments to specific adapters

```js
const api.layout = {
  adapters: {
    memory: api.adapters.memory,
    remote: api.adapters.remote,
    graphql: api.adapters.graphql
  },
  local: {
    dev: 'memory.map',
    test: 'sync.localstorage',
    prod: 'sync.amplify',
  },
  remote: {
    dev: 'memory.graphql',
    test: 'graphql.test',
    prod: 'graphql.prod',
  }
}
```

### GraphQL adapter

```js
const graphQL = {
  $Single: {
    update() {
      mutate({ action: "update", type, data });
    },
    read({ name, props, query }) {
      query({ name, props, query });
    }
  },
  $List: {
    add({ type, data }) {
      mutate({ action: "add", type, data });
    }
  },
  $Entity: {
    $extends: [api.$Single, api.$List]
  },
  Person: {
    $extends: [api.$Entity]
  }
};
```
