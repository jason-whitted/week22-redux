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

```diff
const App = () => {
+ const [text, setText] = useState("");
+ const [color, setColor] = useState("");
```

Then we need to pass the values down to the tree to the appropriate children.

```diff
return (
  <div className="container mt-3">
-   <Settings />
-   <Preview />
+   <Settings text={text} setText={setText} color={color} setColor={setColor} />
+   <Preview text={text} color={color} />
  </div>
);
```

The `Settings` component didn't care about the state before. Now it needs to be updated to relay these properties down the chain.

```diff
const Settings = ({ text, setText, color, setColor }) => {
  return (
    <div className="card mb-3">
      <div className="card-header">Settings</div>
      <div className="card-body">
-       <TextField />
-       <ColorField />
+       <TextField text={text} setText={setText} />
+       <ColorField color={color} setColor={setColor} />
      </div>
    </div>
  );
};
```

We also need to update the `TextField` and `ColorField` components to read their values from props.

```diff
-const TextField = () => {
+const TextField = ({ text, setText }) => {
-  const [text, setText] = useState("");
```

```diff
-const ColorField = () => {
+const ColorField = ({ color, setColor }) => {
-  const [color, setColor] = useState("");
```

For each distinct state value we may have to pass two props: `xxx` and `setXxx`. What happens if there were 50 different settings? We'd have to pass 100 props to Settings. Gross!

NOTE: Continiously passing props from parent to children components is referred to as **Prop Drilling**. It's monotonous and makes your React code very verbose and repetative. We'll get to that later :)

But at least now we can update the `Preview` component so that it displays a preview.

```diff
-const Preview = () => {
+const Preview = ({ text, color }) => {
  return (
    <div className="card mb-3">
      <div className="card-header">Preview</div>
-     <div className="card-body">
-       {
-         // TODO: Display a preview of the text/color
-         // specified in Settings
-       }
-     </div>
+     <div className="card-body" style={{ color }}>
+       {text}
+     </div>
    </div>
  );
};
```

The app works now!

https://stackblitz.com/edit/react-eajmcb
