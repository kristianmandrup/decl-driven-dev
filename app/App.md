# Application

The application config should set up global aspects of the application.

## Mini apps

An application config must have a name such as `Dashboard` or `Products`
The full app can consist of multiple smaller apps (micro apps) which are typically loaded on demand on the route level.

Each app may use a separate State management system, so that one app uses MobX and another uses Redux. Each app can then listen to events and actions using the same _Event Bus_, typically RxJS.

Each app can be developed and tested individually by separate teams if needed.

Each app can be seen as a `display` with one app as the root display.

## Maturity tag

Each application configuration can be assigned a maturity tag such as:

- prototype
- alpha
- beta
- rc (release candidate)
- prod

## Environments

An app can be tagged with an environment, one of:

- dev
- staging
- prod

## Factories

Factories can be configured on the app level to act as defaults.
The `components` can be overridden on any `display` if needed.

```js
  factories: {
    components: {
      map: buildComponents,
      single: linkComponent
    },
    actions: {
      map: $actions.createAll,
      single: $actions.createAction
    }
    store: {
      local: $stores.redux.create({
        sagas: true
      },
      remote: $stores.graphQL.createApolloClient({
        url: 'localhost:4000'
      })
    }
  },
```

## Modules

### Application modules

- store
- session

Any display module (acts as default config for any child display)

### Display modules

- data
- components
- displays
- routes
- validators

```js
import { modules } from './factories'
import { factories } from './factories'

const app.dev = createApp({
  name: 'dashboard',
  title: 'Dashboard',
  factories,
  modules,
  layout
})
```
