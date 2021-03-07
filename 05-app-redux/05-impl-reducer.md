# Redux: Implementation

## Reducer

For the reducer we need to specify the reducer function as well as the initial state.

### `store/settings/reducer/initialState.js`

```js
export default {
  text: "",
  color: "",
};
```

### `store/settings/reducer/reducer.js`

For the reducer we need to import all of the constants and also the initial state.

On the first call to the reducer the current `state` may be `undefined`. We can default it to `initialState`.

The second parameter is the action. Every action consists of two properties (`type` and `payload`) and we can just destructure them here.

The reducer should **_NEVER_** mutate the state object!
- Do NOT use assignment statements (=, +=, ++, etc.)
- Do NOT push, pop, shift, unshift, or splice an array that is in state
- Use object rest/spread to return a new object
- Use array.filter to remove items from an array
- Use array rest/spread operators to add items to an array

```js
// BAD!
state.name = "Bob";
state.age++;
state.likes.push("apples");
return state;
```
```js
// Good!
return {
  ...state,
  name: "Bob",
  age: state.age + 1,
  likes: [...state.likes, "apples"],
};
```

The reducer should **_ALWAYS_** return a state object. Don't forget your `default` case!

```js
import * as CONST from "../constants";
import initialState from "./initialState";

export default (state = initialState, { type, payload }) => {
  switch (type) {
    case CONST.SETTINGS_SET_TEXT:
      return {
        ...state,
        text: payload,
      };
    case CONST.SETTINGS_SET_COLOR:
      return {
        ...state,
        color: payload,
      };
    default:
      return state;
  }
};
```

Now we'll create the index.js to export them.

### `store/settings/reducer/index.js`

The term `initialState` and `reducer` is too generic to work if our store has multiple reducers. I usually prefix them here with the name of the reducer.

```js
export { default as settingsInitialState } from "./initialState";
export { default as settingsReducer } from "./reducer";
```
