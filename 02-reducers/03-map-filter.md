# Map + Filter

Let's examine the following code.

```js
const array = ["apple", "banana", "carrot", "date", "eggplant"];
const result = array
  .map(str => text.replace(/[aeiou]/gi, '')),
  .filter(str => str.includes("t"));
```

Just for clarity, lets refactor each one of these transform functions.

```js
const consonants = str => str.replace(/[aeiou]/gi, "");
const mustHaveT = str => str.includes("t");
```

Then we could rewrite the original code using these functions.

```js
const array = ["apple", "banana", "carrot", "date", "eggplant"];
const result = array
  .map(consonants),
  .filter(mustHaveT);
```

Lets first walk through what this is doing.

| Code                 | Result                                              |
| -------------------- | --------------------------------------------------- |
| `array`              | `["apple", "banana", "carrot", "date", "eggplant"]` |
| `.map(consonants)`   | `["ppl", "bnn", "crrt", "dt", "ggplnt"]`            |
| `.filter(mustHaveT)` | `["crrt", "dt", "ggplnt"]`                          |

We have new items in the resulting array AND we have a different number of results.

- `filter` always returns objects from the original array
- `map` always returns an array of the same length as the original

Here we have an outcome that cannot be done by just `filter` or by just `map`.

And subsequently we cannot use fancy `compose` and boolean `and` functions to fix the problem here.

The super-convenient `filter` and `map` functions are handcuffing us. Dagnabbit!
