# Redux: Implementation

## Constants

I usually start by defining the constants since both the action creators and the reducer will use them.

The constants must be unique across ALL of the reducers. I normally prefix them with the name of the reducer.

### `store/settings/constants/index.js`

```js
export const SETTINGS_SET_COLOR = "Settings: Set Color";
export const SETTINGS_SET_TEXT = "Settings: Set Text";
```
