# Session

Registration and Login

## Objective

Make it as easy as Amplify using various pluggable Session providers (adapters):

- Firebase
- Amplify (Via AWS Cognito)
- Auth0
- ...

## Registration

## Login

## Session providers

```js
import { amplify } from "./config";

export const providers = {
  amplify
};
```

### Amplify Session provider

```js
import { config } from "./config";

// adapter is the actual function that can adapt and provide the session given the configuration
import { adapter } from "./adapter";

export const amplify = {
  type: "provider",
  name: "amplify",
  adapter,
  config
};
```

### Amplify adapter

```js
export const function(config = {}): Session {
  //
  // return session
}
```

### Adapter config

```js
export const config = {
  name: "simple",
  // to ensure it is only used for amplify adapter
  adapter: "amplify",
  contexts: {
    registration: {
      // ...
    },
    login: {
      // ...
    }
  }
};
```
