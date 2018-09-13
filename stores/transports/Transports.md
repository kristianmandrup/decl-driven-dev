# Transports

A transport layer can be used to sync local and remote stores.

Typically a transport could be setup to make REST requests posting data from the client to the server, while having a Web socket connection, subscribing to changes from the server used to update the local client store.

## Sync local updates to server store

Sample `saveHandler`

```js
this.saveHandler = reaction(
  // observe everything that is used in the JSON:
  () => this.asJson,
  // if autoSave is on, send json to server
  json => {
    if (this.autoSave) {
      this.store.transportLayer.saveTodo(json);
    }
  }
);
```

## Sync remote updates to client store

```js
  updateTodoFromServer(json) {
    var todo = this.todos.find(todo => todo.id === json.id);
    if (!todo) {
      todo = new Todo(this, json.id);
      this.todos.push(todo);
    }
    if (json.isDeleted) {
      this.removeTodo(todo);
    } else {
      todo.updateFromJson(json);
    }
  }
```
