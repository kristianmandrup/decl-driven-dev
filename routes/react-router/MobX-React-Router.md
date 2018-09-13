# mobx react router

See [mobx-react-router](https://www.npmjs.com/package/mobx-react-router)

## Example

```js
import React from "react";
import ReactDOM from "react-dom";
import createBrowserHistory from "history/createBrowserHistory";
import { Provider } from "mobx-react";
import { RouterStore, syncHistoryWithStore } from "mobx-react-router";
import { Router } from "react-router";
import App from "./App";

const browserHistory = createBrowserHistory();
const routingStore = new RouterStore();

const stores = {
  // Key can be whatever you want
  routing: routingStore
  // ...other stores
};

const history = syncHistoryWithStore(browserHistory, routingStore);

ReactDOM.render(
  <Provider {...stores}>
    <Router history={history}>
      <App />
    </Router>
  </Provider>,
  document.getElementById("root")
);
```

App.js

```js
import React, { Component } from "react";
import { inject, observer } from "mobx-react";

@inject("routing")
@observer
export default class App extends Component {
  render() {
    const { location, push, goBack } = this.props.routing;

    return (
      <div>
        <span>Current pathname: {location.pathname}</span>
        <button onClick={() => push("/test")}>Change url</button>
        <button onClick={() => goBack()}>Go Back</button>
      </div>
    );
  }
}
```
