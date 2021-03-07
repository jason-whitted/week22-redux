# Solution: useState

Our app is currently set up with this structure:

```
App
  Settings
    TextField*
    ColorField*
  Preview
```

- The `text` state is stored in the `TextField`
- The `color` state is stored in the `ColorField`

In order for the `Preview` to know about the values we need to raise the state up to the closest parent element -- `App` in this example.

```js
const App = () => {
  const [text, setText] = useState("");
  const [color, setColor] = useState("");
```

Then we need to pass the values down to the tree to the appropriate children.

```js
return (
  <div className="container mt-3">
    <Settings text={text} setText={setText} color={color} setColor={setColor} />
    <Preview text={text} color={color} />
  </div>
);
```

The `Settings` component didn't care about the state before. Now it needs to be updated to relay these properties down the chain.

```js
const Settings = ({ text, setText, color, setColor }) => {
  return (
    <div className="card mb-3">
      <div className="card-header">Settings</div>
      <div className="card-body">
        <TextField text={text} setText={setText} />
        <ColorField color={color} setColor={setColor} />
      </div>
    </div>
  );
};
```

For each distinct state value we may have to pass two props: `xxx` and `setXxx`. What happens if there were 50 different settings? We'd have to pass 100 props to Settings. Gross!

NOTE: Continiously passing props from parent to children components is referred to as **Prop Drilling**. It's monotonous and makes your React code very verbose and repetative. We'll get to that later :)

https://stackblitz.com/edit/react-eajmcb
