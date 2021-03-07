# App

```js
const App = () => {
  return (
    <div className="container mt-3">
      <Settings />
      <Preview />
    </div>
  );
};
```

```js
const Settings = () => {
  return (
    <div className="card mb-3">
      <div className="card-header">Settings</div>
      <div className="card-body">
        <TextField />
        <ColorField />
      </div>
    </div>
  );
};
```

```js
const TextField = () => {
  const [text, setText] = useState("");

  return (
    <div className="form-group">
      <label>Text:</label>
      <input
        type="text"
        className="form-control"
        value={text}
        onChange={e => setText(e.target.value)}
      />
    </div>
  );
};
```

```js
const colors = ["black", "red", "orange", "yellow", "green", "blue"];

const ColorField = () => {
  const [color, setColor] = useState(colors[0]);

  return (
    <div className="form-group">
      <label>Color:</label>
      <select
        className="form-control"
        value={color}
        onChange={e => setColor(e.target.value)}
      >
        {colors.map(color => (
          <option key={color}>{color}</option>
        ))}
      </select>
    </div>
  );
};
```

```js
const Preview = () => {
  return (
    <div className="card mb-3">
      <div className="card-header">Preview</div>
      <div className="card-body">
        {
          // TODO: Display a preview of the text/color
          // specified in Settings
        }
      </div>
    </div>
  );
};
```

https://stackblitz.com/edit/react-xdt4qb
