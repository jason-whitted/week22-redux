# Redux: Implementation

## Hooks

The `react-redux` library provides two primary hooks:

- `useDispatch`
  - > This hook returns a reference to the dispatch function from the Redux store. You may use it to dispatch actions as needed.
- `useSelector`
  - > Allows you to extract data from the Redux store state, using a selector function.

Let's see these in action in a component like `TextField`.

### `TextField.js`

```js
import React from "react";
import { useDispatch, useSelector } from "react-redux";
import { setText, selectText } from "./store";

const TextField = () => {
  const dispatch = useDispatch();
  const text = useSelector(selectText);

  return (
    <div className="form-group">
      <label>Text:</label>
      <input
        type="text"
        className="form-control"
        value={text}
        onChange={e => dispatch(setText(e.target.value))}
      />
    </div>
  );
};

export default TextField;
```

NOTE: Notice there are no props being passed into this component. The `useDispatch` and `useSelector` hooks are reading them from the context provided by the `Provider` in the root index.js file.

Our code is very clean now. All of the components that rely on the data from the store are automatically re-rendered any time any of the data that they care about is changed. It just works -- like magic!

![](https://3starlearningexperiences.files.wordpress.com/2018/12/giants.jpg?w=620)

https://stackblitz.com/edit/react-5ivsgw
