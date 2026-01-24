# Flaten Array

Below is an interview question:

## Metadata

- Company: Accolite
- Profile: Angular Developer
- Round: 2nd
- Date: 2025-12-31 15:30 to 16:30

```js
// flatten array

// let arr = [1,[3,4,[3,4],8],13];
// let arr = [1, [3,4,[3,4],8], 13];
let arr = [1, undefined, [2], null, 3];

let resultArr = [];

function flattenArray(arr) {
  if (typeof arr == "number") {
    resultArr.push(arr);
  } else if (Array.isArray(arr)) {
    for (let i = 0; i < arr.length; i++) {
      flattenArray(arr[i]);
    }
  }
}

flattenArray(arr);
console.log(resultArr);
```

_Note_

- I missed to declare i with let, resulting to ambiguity in the final result, missing one or two last elements
