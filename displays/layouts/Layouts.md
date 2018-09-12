# Layouts

Layouts are used to indicate how to layout displays and components in a specific configuration.
A layout should mostly specify a number of slots than can then be filled with displays.

The layot should indicate relative positioning (structure) of the items placed in the slots.
A slot may also have a reference to a default display to be used for the slot if no item is provided.

A layout has the following properties

- `name` of the layout used to reference it
- `positioner` name of a registered function (with a strategy) which can do the actual positioning
- `themer` name of a function which can theme the displays and components used, such as for Material Design etc.
- `slots` map of slots

## Positioner

The `positioner` may differ across various environments. In one case, the items will be laid out horizontally, while in another vertically.

## Themer

The `themer` is used to theme the layout, such as creating the `appDrawer` using a Material UI Drawer component.

## Slots

Sots is a map of slots, where each slot can take a named display and indicates its relative position. The themer and positioner will act to place and theme the item accordingly.

### Slot

A layout slot contains:

- `position`
- `display`

The position is the default relative position and the display is the default display to render in the slot.

```js
'appBar': {
  position: 'first',
  display: 'appBar'
},
```

#### Position

- `first`
- `last`
- `after` a named display in the list of items
- `before`

If no position is given it will be rendered last.
If two or more items are `before` or `after` the same item, they will be rendered in whatever order the positioner decides (usually "first served"). Same goes for multiple `first` and `last`.

#### Display

Reference to a named display

## Application layout example

```js
{
  name: 'dashboard',
  positioner: 'stack',
  themer: 'material-ui',
  slots: {
    'appBar': {
      position: 'first',
      display: 'appBar'
    },
    'drawer': {
      after: 'appBar',
      display: 'appDrawer'
    },
    'content': {
      position: {
        after: 'appBar',
      },
      display: 'routes'
    },
    'footer': {
      position: 'last',
      display: 'footer'
    }
  }
}
```

```js
import { dashboard } from "./dashboard";
import { application } from "./application";

const layouts = {
  application,
  dashboard
};
```
