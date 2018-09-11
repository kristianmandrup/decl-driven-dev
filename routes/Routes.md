# Routes

The `Router` is a top-level app entity, injected via `withRouter()` HOC to make it available for all nested children if/when needed.

The app will usually have different named route sections, such as for master-detail views of different entities

```js
const routes = {
  type: 'react-router',
  named: {
    app: {
      name: "appRouter",
      routes: {
        home: {
          // path: '/'
        },
        dashboard: {
          path: "dashboard",
          display: 'dashboard'
        },
        products: {
          path: "products"
          display: 'products'
        }
      }
    },
    products: {
      name: "productsRouter",
      routes: {
        products: {
          path: "/products",
          display: 'products.list'
        },
        product: {
          path: "/product/:id"
        }
      }
    },
    product: {
      name: "productRouter",
      routes: {
        item: {
          path: "/products/:id",
          display: 'product'
        },
        comments: {
          path: "/product/:id/comments"
        },
        comments: {
          path: "/product/:id/images"
        }
      }
    },
    productComment: {
      comments: {
        path: "/product/:id/comments/:id"
      }
    }
  }
};
```

## Use routes in displays

```js
layouts["nav-list"] = {
  base: "list",
  display: {
    // may use flex to position items
    controls: {
      position: 'top',
      style: 'row',
      actions: ["filter", "sort"],
    }
    view: {
      position: 'center',
      style: 'fill',
      display: ["router"],
    },
    controls: {
      style: 'row',
      position: 'bottom',
      actions: ["cursor"]
    }
  }
};
```

```js
const display = {
  generic: {
    collection: {
      list: {
        mapping: {
          filter: "text-query",
          sort: false,
          router: "$type",
          cursor: "pagination",
          select: "listItem" // what to display when list item selected
        },
        layout: {
          base: 'nav-list', //display using navigatable list
          use: [
            'filter',
            'sort',
            'router'
            'cursor'
            'select'
          ],
        }
      }
    }
  }
}
```

```js
  products: {
    default: 'list',
    list: {
      mapping: {
        filter: "text-query",
        sort: false,
        routes: "products",
        cursor: "pagination",
        select: "product.listItem" // what to display when list item selected
      },
      layout: {
        base: 'nav-list', //display using navigatable list
        use: [
          'filter',
          'sort',
          'router'
          'cursor'
          'select'
        ]
    },
    grid: {
      base: 'nav-grid'
      // ...
    }
  },
  product: {
    layouts: {
      views: {}
    },
    instances: {
      listItem: {
        routes: "product"
      }
    }
  }
};
```
