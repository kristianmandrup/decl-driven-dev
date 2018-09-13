# Router

Simple router->state->view flow example

## Director

```js
import { Router } from 'director'

export function startRouter(store) {
  const router = new Router({
    'documents/:id': (id) => store.showDocument(id)
    'documents/*': () => store.showOverview()
  }).configure({
    notfound: () => store.showOverview(),
    html5history: true
  })
}
```

MobX store

```js
@action showOverview() {
    this.currentView = {
        name: "overview",
        documents: fromPromise(fetch(`/json/documents.json`))
    }
}
```

Test

```js
test("it should be possible to open the documents overview", t => {
  const viewStore = new ViewStore();
  viewStore.showOverview();
  t.equal(viewStore.currentView.name, "overview");
  const docs = viewStore.currentView.documents;
  when(
    () => docs.state !== "pending",
    () => {
      t.equal(docs.state, "fulfilled");
      t.equal(docs.value.length, 2);
      t.end();
    }
  );
});
```

App, using currentView

```js
const App = observer(({ viewStore }) => {
  const view = viewStore.currentView;
  switch (view.name) {
    case "overview":
      return <DocumentOverview documents={view.documents} />;
    default:
      return <PageNotFound />;
  }
});
```

Rendering app to history

```js
@computed get currentPath() {
    switch(this.currentView.name) {
        case "overview": return "/document/"
        case "document": return `/document/${this.currentView.documentId}`
    }
}

autorun(() => {
    const path = viewStore.currentPath
    if (path !== window.location.pathname)
            window.history.pushState(null, null, path)
})
```
