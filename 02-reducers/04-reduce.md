# Reduce

> **Array.prototype.reduce()**<br>
> The **reduce()** method executes a **reducer** function (that you provide) on each element of the array, resulting in single output value.

## Syntax

```js
arr.reduce(reducer, initialValue);
```

The `reducer` is a callback function that has the following signature:

```js
(accumulator, currentValue) => newValue;
```

> Your **reducer** function's returned value is assigned to the accumulator, whose value is remembered across each iteration throughout the array, and ultimately becomes the final, single resulting value.

Both the `filter` and `map` functions always return arrays. That is not the case with a reduce function. As we will see in examples below, we can use reducers to completely transform an array into another data type.

## Examples

### Summing

```js
const sum = (total, current) => total + current;
const numbers = [1, 1, 2, 3, 5, 8];
const result = numbers.reduce(sum, 0);
```

Iterations:

| input     | output |
| --------- | -----: |
| `(0, 1)`  |      1 |
| `(1, 1)`  |      2 |
| `(2, 2)`  |      4 |
| `(4, 3)`  |      7 |
| `(7, 5)`  |     12 |
| `(12, 8)` |     20 |

### Max Value

```js
const max = (a, b) => (a > b ? a : b);
const numbers = [1, -1, 2, -3, 5, -8];
const result = numbers.reduce(max, Number.MIN_VALUE);
```

Iterations:

| input                   | output |
| ----------------------- | -----: |
| `(Number.MIN_VALUE, 1)` |      1 |
| `(1, -1)`               |      1 |
| `(1, 2)`                |      2 |
| `(2, -3)`               |      2 |
| `(2, 5)`                |      5 |
| `(5, -8)`               |      5 |

### Mapping

```js
const appendConsonants = (arr, str) => {
  const s = str.replace(/[aeiou]/gi, "");
  arr.push(s);
  return arr;
};
const array = ["apple", "banana", "carrot", "date", "eggplant"];
const result = array.reduce(appendConsonants, []);
```

Iterations:

| input                                        | output                                   |
| -------------------------------------------- | ---------------------------------------- |
| `([], "apple")`                              | `["ppl"]`                                |
| `(["ppl"], "banana")`                        | `["ppl", "bnn"]`                         |
| `(["ppl", "bnn"], "carrot")`                 | `["ppl", "bnn", "crrt"]`                 |
| `(["ppl", "bnn", "crrt"], "date")`           | `["ppl", "bnn", "crrt", "dt"]`           |
| `(["ppl", "bnn", "crrt", "dt"], "eggplant")` | `["ppl", "bnn", "crrt", "dt", "ggplnt"]` |

### Filtering

```js
const appendWithPorR = (arr, str) => {
  if (str.includes("p") || str.includes("r")) {
    arr.push(str);
  }
  return arr;
};
const array = ["apple", "banana", "carrot", "date", "eggplant"];
const result = array.reduce(appendWithPorR, []);
```

Iterations:

| input                               | output                            |
| ----------------------------------- | --------------------------------- |
| `([], "apple")`                     | `["apple"]`                       |
| `(["apple"], "banana")`             | `["apple"]`                       |
| `(["apple"], "carrot")`             | `["apple", "carrot"]`             |
| `(["apple", "carrot"], "date")`     | `["apple", "carrot"]`             |
| `(["apple", "carrot"], "eggplant")` | `["apple", "carrot", "eggplant"]` |

### Map + Filter

```js
const appendConsonantsWithPorR = (arr, str) => {
  if (str.includes("p") || str.includes("r")) {
    const s = str.replace(/[aeiou]/gi, "");
    arr.push(s);
  }
  return arr;
};
const array = ["apple", "banana", "carrot", "date", "eggplant"];
const result = array.reduce(appendConsonantsWithPorR, []);
```

Iterations:

| input                           | output                      |
| ------------------------------- | --------------------------- |
| `([], "apple")`                 | `["ppl"]`                   |
| `(["ppl"], "banana")`           | `["ppl"]`                   |
| `(["ppl"], "carrot")`           | `["ppl", "crrt"]`           |
| `(["ppl", "crrt"], "date")`     | `["ppl", "crrt"]`           |
| `(["ppl", "crrt"], "eggplant")` | `["ppl", "crrt", "ggplnt"]` |

## Summary

Anything you can do in any number or combination of `filter` / `map` functions you can do in a single `reducer` function!

Reducers are powerful. Long live reducers!

Reducers take a bit more cognitive load to comprehend when reading code. You do not need to outright avoid `map` and `filter` in favor of `reduce`. The `map` and `filter` methods are inherantly more readable.
