# Entity

Define a full entity by extending from multiple types of entity models/schemas

- [JSON](./JSON.md)
- [Generators](./Generators.md)

## Implied format

Using all defaults (conventions)

```js
{
  type: 'Person',
}
```

## Explicit

```js
{
  type: 'Person',
  // use Person.json JSON schema
  schema: 'Person'
  actions: 'Person'
  // views of data
  views: 'Person'
}
```

## Advanced

```js
{
  type: 'Person',
  // use Person.json JSON schema
  schema: {
    $extends: ['Person'],
    // extensions here
  },
  // actions reduce/transform state
  actions: {
    // default
    $extends: ['Person'],
    // extensions here
  },
  // views of data
  views: {
    // default
    $extends: ['Person'],
    // extensions here
  }
}
```
