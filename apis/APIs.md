# API

APIs are used to operate on collection/entity adapters

```js
import { memory } from "./memory";
const api = {
  memory
};
```

## Properties

- `init` method to initialize the api
- `addType` method to add a type, similar to a DB table schema
- `actions` actions that can be performed on api/storage

### Actions

PS: Use currying to avoid passing the type argument

### Generic

- `list({type})` get the full collection
- `retrieve({type, id})` retrieve specific item in collection
- `indexOf({type, id})` get index of item in collection (implicit for indexed collections such as maps)

### Collection

- `add({ type, item })` Add an item (`item`) to the collection
- `remove({ type, id?, item? })` Remove an item from the collection
- `fetch({ type, filter })` Fetch items passing filter from the collection

### Item

- `update({type, id, item})`
- `delete({type, id, item})`
- `get({type, id, item, name})` get named property (can be a child collection) of item

## Memory

```js
import { list } from "./list";
import { map } from "./map";
import { graphql } from "./graphql";

const memory = {
  init() {
    this.collections = {};
  },
  named: {
    list,
    map,
    graphql
  }
};
```

### Example: List

It is recommended to use maps instead of lists as collections, as maps are inherently indexed much like a DB index for a DB table. Lookups in lists are much slower as you have to iterate through the entire list to find an entry with a matching key.

```js
{
  init() {
    this.collections.lists = {};
  },
  addType(type) {
    this.collections.lists[type] = [];
  },
  actions: {
    generic: {
      list({type}) {
        return this.collections.lists[type];
      },
      retrieve({type, id}) {
        return this.list({type}).find(item => item.id === id)
      },
      indexOf({type, id}) {
        const item = this.retrieve({type, id})
        return item && item.id
      },
    },
    collection: {
      add({ type, item }) {
        const list = this.list({type})
        list && list.push(item);
      },
      remove({ type, id, item }) {
        id = id || item.id
        const list = this.list({type})
        const index = this.indexOf({type, id})
        index && list.slice(index, 1)
      },
      fetch({ type, filter }) {
        const list = this.list({type})
        return list.filter(filter)
      }
    },
    item: {
      update({type, id, item}) {
        id = id || item.id
        const item = this.retrieve({type, id})
      },
      delete({type, id, item}) {
        id = id || item.id
        return this.list.remove({type, id})
      },
      get({type, id, item, name}) {
        const item = this.retrieve({type, id})
        return item[name]
      }
    }
  }
}
```

### Example: Map

```js
const map = {
  init() {
    this.collections.maps = {};
  },
  addType(type) {
    this.collections.maps[type] = {};
  },
  actions: {
    generic: {
      // ...
    },
    collection: {
      add({ type, item }) {
        const map = this.collections.maps[type];
        list && list.push(item);
      }
      // ...
    },
    item: {
      // ...
    }
  }
};
```

### Local GraphQL

```js
const graphQL = {
  init() {
    // this.mutations = ...
  },
  addType(type) {
    this.collections.types[type] = gqlType(type);
  },
  actions: {
    collection: {
      add({ type, item }) {
        this.mutations[type].update(item);
      }
    }
  }
};
```

## Server

- GraphQL
- ...

### Remote GraphQL

You could extend another GraphQL config

```js
import { logActions } from './middleware'

const graphQL = {
  extends: 'memory.graphql'
  init() {
    // this.mutations = ...
  },
  middleware: {
    logActions
  }
};
```
