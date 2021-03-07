# Solution: useReducer

Rather than keeping track of individual state items, we could move them all into a single object.

```js
const initialState = {
  text: "",
  color: "",
};
```

Cool. Now if we have 50 properties we still only have one `state` object that we will have to pass around. We just got rid of 49 props that we no longer need to pass around!

We still have to pass around 50 different `setXxx`, `setYyy` methods though. Right?

Let's make any update to the state a generic object, called an "action". An action will only have two properties:

```js
const action = {
  type: String, // A pre-defined indicator of the type of update
  payload: Any, // Any data that needs to be passed as part of the update
};
```

In our current case we'll need two constants defined for our action types.

```js
const SET_TEXT = "SET_TEXT";
const SET_COLOR = "SET_COLOR";
```

Then we can create a single method to handle these update actions, called "dispatch".

If we can follow this approach then we only need to pass a single `dispatch` method down instead of 50 `setXxx` methods. We just got rid of 49 more props!

Now what we need to do is create a reducer function which will be responsible for receiving a dispatched action and updating the state.

IMPORTANT: React renders only when props change. You should never, ever, EVER mutate a state object. You should always return a new object so that React knows it needs to re-render.

Our reducer will have the signature:

```js
(currentState, action) => newState;
```

```js
const reducer = (state = initialState, { type, payload }) => {
  switch (type) {
    case SET_TEXT:
      return {
        ...state,
        text: payload,
      };
    case SET_COLOR:
      return {
        ...state,
        color: payload,
      };
    default:
      return state;
  }
};
```

## The Solution

We can set up the App to use a reducer to manage the state. Then we only need to pass down the `state` and the `dispatch` function to components that need it.

```diff
const App = () => {
- const [text, setText] = useState("");
- const [color, setColor] = useState("");
+ const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div className="container mt-3">
-     <Settings text={text} setText={setText} color={color} setColor={setColor} />
-     <Preview text={text} color={color} />
+     <Settings state={state} dispatch={dispatch} />
+     <Preview state={state} />
    </div>
  );
};
```

Components that need to update the state, like `TextField`, just need to `dispatch` an action.

```diff
-const TextField = ({ text, setText }) => {
+const TextField = ({ state, dispatch }) => {
  return (
    <div className="form-group">
      <label>Text:</label>
      <input
        type="text"
        className="form-control"
-       value={text}
+       value={state.text}
-       onChange={e => setText(e.target.value)}
+       onChange={e =>
+         dispatch({
+           type: SET_TEXT,
+           payload: e.target.value,
+         })
+       }
      />
    </div>
  );
};
```

https://stackblitz.com/edit/react-rnz32p
