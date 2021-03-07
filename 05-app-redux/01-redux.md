# Redux

> **Redux**<br/>
> A Predictable State Container for JS Apps

**Redux** mainstreamed many of the concepts that are vital in modern React code:

- Read
  - **immutable** global state object
- Create/Update/Delete
  - dispatch actions to a reducer for update

You create a "store" by specifying one or more reducer(s). The store manages the state for you via the `getState()` and `dispatch()` methods.

The `react-redux` library provides React-specific implementations for Redux. The context is abstracted behind the `Provider` component and the `useDispatch` and `useSelector` hooks.

```bash
npm add redux react-redux
```
