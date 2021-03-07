# Redux: Implementation

## Exporting the reducer

We have exports for the actions, constants, reducer, and selectors. We do not yet exporting all of them for the reducer. Let's take care of that.

### `store/settings/index.js`

```js
export * from "./actions";
export * from "./constants";
export * from "./reducer";
export * from "./selectors";
```

## Root Reducer

Redux's store is a single state object, managed by a single reducer.

> As your app grows more complex, you'll want to split your reducing function into separate functions, each managing independent parts of the state.
>
> The `combineReducers` helper function turns an object whose values are different reducing functions into a single reducing function you can pass to `createStore`.

Almost every production implementation uses `combineReducers`. In this app we could skip over this for simplicity, but it is so common place it is better to implement it instead of avoiding it.

### `store/rootReducer.js`

```js
import { combineReducers } from "redux";
import { settingsReducer as settings } from "./settings";

export default combineReducers({
  settings,
  // additional reducers can be added here
});
```

NOTE: This is the reason that our selector functions looked like this:

```js
// Right! Here `state` is the GLOBAL state.
export default state => state.settings.text;
```

instead of:

```js
// WRONG!
export default state => state.text;
```

But inside of the settings reducer we referred to just:
```js
// Right!  Here `state` is the LOCAL state.
// (i.e. just the `settings` portion of the GLOBAL state)
return {
  ...state,
  color: payload,
};
```

Instead of:
```js
// WRONG!
return {
  ...state,
  settings: {
    ...state.settings,
    color: payload,
  }
}
```

TL;DR
- In a `reducer` the state is LOCAL
- In a `selector` the state is GLOBAL


### `store/index.js`
And finally we can create the Redux store and export it (and everything else)!

```js
import { createStore } from "redux";
import rootReducer from "./rootReducer";

export * from "./settings";

export default createStore(rootReducer);
```
