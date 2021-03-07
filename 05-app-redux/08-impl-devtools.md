# Redux: Implementation

## Redux DevTools

I always recommend the Redux DevTools chrome extension.

To configure it we just need to modify our `createStore` section.

### `store/index.js`

```js
export default createStore(
  rootReducer,
  /* preloadedState, */
  window.__REDUX_DEVTOOLS_EXTENSION__?.()
);
```
