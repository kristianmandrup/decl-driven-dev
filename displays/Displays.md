# Displays

```js
const displays = {
  dashboard: {},
  contact: {},
  entity: {
    user: {
      views: {
        registration: {},
        login: {}
      },
      routes: {
        registration: [
          'registration'
        ],
        login: [
          'login'
        ]
      }
    },
    products: {
      views: {
        browseAll: {
          list: {
            filter: 'user',
            layout: 'products'
          },
        },
        recommended: {
          list: {
            filter: 'recommended',
            layout: 'products'
          }
        },
      },
      routes: {
        root: [
          'recommended',
          'browseAll'
        ],
        recommended: [
          'recommended'
        ]
      ]
    },
    product: {
      form: {}
    }
    // ...
  }
};
```
