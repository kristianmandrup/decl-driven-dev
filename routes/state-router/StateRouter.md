# State Router

## Dumb UI: create a view store

- Capture crucial app state in a browser unaware store
- UI just renders this state
- Browser url / history is just another derivation
- Navigation triggers state changes instead of component hooks

## Recipe

- Routes trigger state updates
- State updates auto-trigger view updates via observables
- Views determine what to render based on new state received

From [MobX patterns](http://mobx-patterns.surge.sh/#73)

See [How to decouple state and UI](https://hackernoon.com/how-to-decouple-state-and-ui-a-k-a-you-dont-need-componentwillmount-cc90b787aa37)

## Libraries

- [mobx-react-router](https://www.npmjs.com/package/mobx-react-router)
- [mobx-location](https://www.npmjs.com/package/mobx-location)

## Example configs

```js
const routes = {
  app: {
    name: "appRouter",
    store: 'viewStore',
    routes: {
      home: {
        path: '/',
        effect: ({id}) => (
          this.store.showHome()
        )
      },
      product:
        path: "products/:id",
        effect: ({id}) => (
          this.store.showProduct(id)
        )
      },
      products: {
        path: "products",
        effect: ({id}) => (
          this.store.showProducts()
        )

      }
    }
  },
```

## Router state actions

```js
@action showProducts() {
    this.currentView = {
        name: "products",
        products: api.fetch({type: 'products'})
    }
}
```

## Display products

```js
function isView(view, name) {
  return view.name == name;
}

const products = (view) => (
  isView(view, 'products') && <ProductList products={view.products} />)
)

const default = (view) => <PageNotFound />;

views = ['products', 'default']

const App = observer(({ viewStore }) => {
  const view = viewStore.currentView;
  // find first view that matches view and render it
  return views.find(v => v(view))
});
```
