# React GraphQL Apollo

Super good tutorial

- [How to GraphQL](https://www.howtographql.com/react-apollo/1-getting-started/)

Packages:

- `apollo-boost` offers some convenience by bundling several packages you need when working with Apollo Client:
- `apollo-client`: Where all the magic happens
- `apollo-cache-inmemory`: Our recommended cache
- `apollo-link-http`: An Apollo Link for remote data fetching
- `apollo-link-error`: An Apollo Link for error handling
- `apollo-link-state`: An Apollo Link for local state management
- `graphql-tag`: Exports the `gql` function for your queries & mutations
- `react-apollo` contains the bindings to use Apollo Client with React.
- `graphql` contains Facebook’s reference implementation of GraphQL - Apollo Client uses some of its functionality as well.

### Simple example

- [Setting Up React with GraphQL](https://www.youtube.com/watch?v=jDvOauhkEOM)

## App

```js
import React from "react";
import ReactDOM from "react-dom";
import {
  ApolloClient,
  createNetworkInterface,
  ApolloProvider
} from "react-apollo";

import Routes from "./routes";
import registerServiceWorker from "./registerServiceWorker";

const networkInterface = createNetworkInterface({
  uri: "http://localhost:8081/graphql"
});

const client = new ApolloClient({
  networkInterface
});

const App = (
  <ApolloProvider client={client}>
    <Routes />
  </ApolloProvider>
);

ReactDOM.render(App, document.getElementById("root"));
registerServiceWorker();
```

## Routes

```js
import React from "react";
import { BrowserRouter, Route, Switch } from "react-router-dom";

import Home from "./Home";

export default () => (
  <BrowserRouter>
    <Switch>
      <Route path="/" exact component={Home} />
    </Switch>
  </BrowserRouter>
);
```

## Home

```js
import React from "react";
import { gql, graphql } from "react-apollo";

const Home = ({ data: { allUsers = [] } }) =>
  allUsers.map(u => <h1 key={u.id}>{u.email}</h1>);

const allUsersQuery = gql`
  {
    allUsers {
      id
      email
    }
  }
`;

export default graphql(allUsersQuery)(Home);
```
