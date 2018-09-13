# Config

Global configs

Used to configure access to various external services, such as servers, cloud services, SaaS solutions etc.

```js
import { dev } from "./dev";

export const config = {
  dev,
  staging,
  prod
};
```

## Dev environment

```js
import { aws } from "./aws";
import { graphql } from "./graphql";
// ...

export const dev = {
  aws,
  graphql
  // ...
};
```

### AWS configs

```js
import { cognito } from "./cognito";
import { amplify } from "./amplify";
// ...

export const dev = {
  amplify,
  cognito
  // ...
};
```
