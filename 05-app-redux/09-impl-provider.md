# Redux: Implementation

## Provider

The `react-redux` library provides a `Provider` which manages the context for us. This is typically added in the root index.js file.

### `index.js`
```js
import React from "react";
import ReactDOM from "react-dom";
import { Provider as ReduxProvider } from "react-redux";

import App from "./App";
import store from "./store";

ReactDOM.render(
  <ReduxProvider store={store}>
    <App />
  </ReduxProvider>,
  document.getElementById("root")
);
```
