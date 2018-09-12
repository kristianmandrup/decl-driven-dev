# Collection display

## Layouts

- list
- grid

## Styling and Theming

A layout can be provided a styler (which components to use) and a theme via providers.

## Example entity collection display

```js
import { list } from "./list";
export const collection = {
  collection: {
    list: {
      // just a few primary attributes
      short: list.short,
      // most of the attributes
      // just reuse short version for now
      long: {
        display: {
          extends: list.short,
          with: {
            // ..
          }
        }
      }
    table: {}
  },
```
