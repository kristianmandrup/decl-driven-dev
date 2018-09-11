# API

APIs are used to operate on collection/entity adapters

```js
const api = {
  memory: {
    list: {
      init() {
        this.collections = {}
        this.collections.lists = {}
      },
      addType(type) {
        this.collections.lists[type] = []
      },
      actions: {
        add({type, obj}) {
          const list = this.collections.lists[type]
          list && list.push(obj)
        }
      }
    },
    map: {
      init() {
        this.collections = {}
        this.collections.maps = {}
      },
      addType(type) {
        this.collections.maps[type] = {}
      },
      actions: {
        add({type, obj}) {
          const map = this.collections.maps[type]
          list && list.push(obj)
        }
      }
    }
    graphql: {
      init() {
        // this.mutations = ...
      },
      addType(type) {
        this.collections.types[type] = gqlType(type)
      },
      actions: {
        add({type, obj}) {
          this.mutations[type].update(obj)
        }
      },
    }
  }
}
```
