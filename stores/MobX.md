# MobX

## Example: Todo store

This store uses a transport layer to connect to a remote api/server to receive notification on store updates which are used to update local cache/store

- `loadTodos()` Fetches all todo's from the server

For each todo received from server, call `updateTodoFromServer` with item data

`fetchedTodos.forEach(json => this.updateTodoFromServer(json))`

Acted upon depending on type of change...

```js
if (json.isDeleted) {
  this.removeTodo(todo);
} else {
  todo.updateFromJson(json);
}
```

```js
import { observable, autorun } from "mobx";
import uuid from "node-uuid";

export class TodoStore {
  authorStore;
  transportLayer;
  @observable
  todos = [];
  @observable
  isLoading = true;

  constructor(transportLayer, authorStore) {
    this.authorStore = authorStore; // Store that can resolve authors for us
    this.transportLayer = transportLayer; // Thing that can make server requests for us
    this.transportLayer.onReceiveTodoUpdate(updatedTodo =>
      this.updateTodoFromServer(updatedTodo)
    );
    this.loadTodos();
  }

  /**
   * Fetches all todo's from the server
   */
  loadTodos() {
    this.isLoading = true;
    this.transportLayer.fetchTodos().then(fetchedTodos => {
      fetchedTodos.forEach(json => this.updateTodoFromServer(json));
      this.isLoading = false;
    });
  }

  /**
   * Update a todo with information from the server. Guarantees a todo
   * only exists once. Might either construct a new todo, update an existing one,
   * or remove an todo if it has been deleted on the server.
   */
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

  /**
   * Creates a fresh todo on the client and server
   */
  createTodo() {
    var todo = new Todo(this);
    this.todos.push(todo);
    return todo;
  }

  /**
   * A todo was somehow deleted, clean it from the client memory
   */
  removeTodo(todo) {
    this.todos.splice(this.todos.indexOf(todo), 1);
    todo.dispose();
  }
}
```

### Store model Todo

The store items can be kept in sync with the remote server store via the transport layer

```js
/**
  * Remove this todo from the client and server
  */
delete() {
    this.store.transportLayer.deleteTodo(this.id);
    this.store.removeTodo(this);
}
```

Each item can have references to the `store` (with transport) and `autoSave` setting.
If `autoSave`, auto matically sync local updates with the store.

```js
  store = null;

  /**
    * Indicates whether changes in this object
    * should be submitted to the server
    */
  autoSave = true;

  /**
    * Disposer for the side effect that automatically
    * stores this Todo, see @dispose.
    */
  saveHandler = null;

  constructor(store, id=uuid.v4()) {
    this.store = store;
    this.id = id;

    this.saveHandler = reaction(
        // observe everything that is used in the JSON:
        () => this.asJson,
        // if autoSave is on, send json to server
        (json) => {
            if (this.autoSave) {
                this.store.transportLayer.saveTodo(json);
            }
        }
    );
  }
```

## Full Todo model class

````js
export class Todo {

    /**
     * unique id of this todo, immutable.
     */
    id = null;

    @observable completed = false;
    @observable task = "";

    /**
     * reference to an Author object (from the authorStore)
     */
    @observable author = null;

    store = null;

    /**
     * Indicates whether changes in this object
     * should be submitted to the server
     */
    autoSave = true;

    /**
     * Disposer for the side effect that automatically
     * stores this Todo, see @dispose.
     */
    saveHandler = null;

    constructor(store, id=uuid.v4()) {
        this.store = store;
        this.id = id;

        this.saveHandler = reaction(
            // observe everything that is used in the JSON:
            () => this.asJson,
            // if autoSave is on, send json to server
            (json) => {
                if (this.autoSave) {
                    this.store.transportLayer.saveTodo(json);
                }
            }
        );
    }

    /**
     * Remove this todo from the client and server
     */
    delete() {
        this.store.transportLayer.deleteTodo(this.id);
        this.store.removeTodo(this);
    }

    @computed get asJson() {
        return {
            id: this.id,
            completed: this.completed,
            task: this.task,
            authorId: this.author ? this.author.id : null
        };
    }

    /**
     * Update this todo with information from the server
     */
    updateFromJson(json) {
        // make sure our changes aren't send back to the server
        this.autoSave = false;
        this.completed = json.completed;
        this.task = json.task;
        this.author = this.store.authorStore.resolveAuthor(json.authorId);
        this.autoSave = true;
    }

    dispose() {
        // clean up the observer
        this.saveHandler();
    }
}```
````
