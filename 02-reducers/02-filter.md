# Filter

We are familiar with the `Array.prototype.filter(predicate)` function.

It's purpose is to remove items from data.

- The original array is not modified
- The original order of the data is preserved in the new array
- The new array will only contain unmodified objects from the original array
- The new array's length will be between 0 and the length of the original array

```js
const array = ["apple", "banana", "carrot", "date", "eggplant"];
const result = array
  .filter(str => str !== "eggplant")
  .filter(str => !str.includes("o"))
  .filter(str => str.length > 4)
  .filter(str => str.split("").reverse().join() !== "elppa")
  .filter(str => !!str);
```

Just for clarity, lets refactor each one of these transform functions.

```js
const noEggplants = str => str !== "eggplant";
const noO = str => !str.includes("o");
const noShorties = str => str.length > 4;
const noElppaBackwards = str => str.split("").reverse().join("") !== "elppa";
const noFalsy = str => !!str;
```

Then we could rewrite the original code using these functions.

```js
const array = ["apple", "banana", "carrot", "date", "eggplant"];
// prettier-ignore
const result = array
  .filter(noEggplants)
  .filter(noO)
  .filter(noShorties)
  .filter(noElppaBackwards)
  .filter(noFalsy);
```

Lets first walk through what this is doing.

| Code                        | Result                                              |
| --------------------------- | --------------------------------------------------- |
| `array`                     | `["apple", "banana", "carrot", "date", "eggplant"]` |
| `.filter(noEggplants)`      | `["apple", "banana", "carrot", "date"]`             |
| `.filter(noO)`              | `["apple", "banana", "date",]`                      |
| `.filter(noShorties)`       | `["apple", "banana"]`                               |
| `.filter(noElppaBackwards)` | `["banana"]`                                        |
| `.filter(noFalsy)`          | `["banana"]`                                        |

- Original array contained 5 items
- `.filter(noEggplants)` - created a new array with 4 items
- `.filter(noO)` - created a new array with 3 items
- `.filter(noShorties)` - create a new array with 2 items
- `.filter(noElppaBackwards)` - created a new array with 1 item
- `.filter(noFalsy)` - created a new array with 1 items

Boolean algebra time! Instead of doing individual filters we could `and` them together.

```js
const nannersOnly = str =>
  noEggplants(str) &&
  noO(str) &&
  noShorties(str) &&
  noElppaBackwards(str) &&
  noFalsy(str);
const result = array.filter(nannersOnly);
```

Heck we could even write an `and` function.

```js
// NOTE: You don't need to understand this code. AT ALL!
const and = (...fns) => x => fns.every(fn => fn(x));
```

The we could rewrite `nannersOnly` as:

```js
const nannersOnly = and(
  noEggplants,
  noO,
  noShorties,
  noElppaBackwards,
  noFalsy
);
```

Just like our first solution, the end result filters out everything except the "banana".

But now we eliminated the creation of 4 arrays.

- Original array contained 5 items
- `.filter(nannersOnly)` - created a new array with 1 item

Imagine if the array contained thousands of items.
