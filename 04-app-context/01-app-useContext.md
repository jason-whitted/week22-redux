# Solution: useContext

Let's say we are working on a component and it needs a custom function. For example, it needs to add two numbers together.

```js
const add = (x, y) => x + y;
```

Now we start working on a second component that needs the same functionality. DRY! Let's not repeat ourselves -- we'll move this function up to a common `add.js` file and now every place that needs it can reference the same function (without having to recreate it or pass it around).

React lets us do the same type of thing. Their solution is referred to as Context, which uses a Provider / Consumer model. The Provider is used to host the data, and the Consumers are the individual components that want to reference the data.

The first step is to create the context in a module that can be referenced by multiple components.

`context.js`
```js
import { createContext } from "react";

export default createContext();
```

The `createContext()` function returns an object with two properties: `Provider` and `Consumer`.

The App will provide the `state` and `dispatch` using the `Provider`.

```diff
+import Context from "./context";

const App = () => {
  const [state, dispatch] = useReducer(reducer, initialState);

+ const context = { state, dispatch };

  return (
+   <Context.Provider value={context}>
      <div className="container mt-3">
-       <Settings state={state} dispatch={dispatch} />
-       <Preview state={state} />
+       <Settings />
+       <Preview />
      </div>
+   </Context.Provider>
  );
};
```

Notice we no longer need to pass the `state` and `dispatch` props down to `Settings` and `Preview`.

A component like `TextField` that needs access to `state` and `dispatch` no longer need to receive props for this. Instead they can use the common `./context.js` module in conjunction with `useContext` to get access to the data.

We can update our Settings component:
```diff
-const Settings = ({ state, dispatch }) => {
+const Settings = () => {
  return (
    <div className="card mb-3">
      <div className="card-header">Settings</div>
      <div className="card-body">
-       <TextField state={state} dispatch={dispatch} />
-       <ColorField state={state} dispatch={dispatch} />
+       <TextField />
+       <ColorField />
      </div>
    </div>
  );
};
```

Much cleaner!

And components like `TextField`, `ColorField`, and `Preview` can be updated to read the data out of context instead of props.

```diff
+import Context from "./context";

-const TextField = ({ state, dispatch }) => {
+const TextField = () => {
+ const { state, dispatch } = useContext(Context);
```

No more Prop Drilling. Context is like magic!

https://stackblitz.com/edit/react-6tiqbq
