# Redux: Implementation

## Actions

Actions are actually action creator functions -- a function that will return an action object.

The user _could_ dispatch an action object directly.

```js
dispatch({ type: "DO_SOMETHING", payload: 123 });
```

But this means that the user has to know about the constants. We could abstract this away from them by providing an action creator.

```js
dispatch(doSomething(123));
```

The action creator pattern is less error prone. Yay!

Let's create the two actions.

### `store/settings/actions/setColor.js`

```js
import * as CONST from "../constants";

export default color => ({
  type: CONST.SETTINGS_SET_COLOR,
  payload: color,
});
```

### `store/settings/actions/setText.js`

```js
import * as CONST from "../constants";

export default text => ({
  type: CONST.SETTINGS_SET_TEXT,
  payload: text,
});
```

Now we'll create the index.js to export them.

### `store/settings/actions/index.js`

```js
export { default as setColor } from "./setColor";
export { default as setText } from "./setText";
```
