# Redux: Implementation

## Selectors

Selectors are functions that _read_ from the state and return a specific value.

They always have the signature:

```js
state => Any;
```

I always prefix my selectors with the word `select`.

### `store/settings/selectors/selectColor.js`

```js
export default state => state.settings.color;
```

### `store/settings/selectors/selectText.js`

```js
export default state => state.settings.text;
```

Now we'll create the index.js to export them.

### `store/settings/reducer/index.js`

```js
export { default as selectColor } from "./selectColor";
export { default as selectText } from "./selectText";
```

NOTE: These names also need to be unique across all reducers. It may be necessary to name them something like `selectSettingsColor` and `selectSettingsText`. I usually try to avoid doing this when I can for clarity.
