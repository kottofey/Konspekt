Уплощает *(не опечатка)* массив, то есть, если есть вложенные подмассивы, то значения из них извлекаются и вставляются в исходный массив

```js
const nested = [1, 2, 3, [4, 5, [6, 7], 8, 9]];
console.log(nested.flat()); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```