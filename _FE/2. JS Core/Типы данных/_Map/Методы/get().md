Достаем значение ключа через метод `.get()`

```js
const map = new Map();

map.set(42, 'число');
map.set('42', 'строка');

console.log(map.get(42)); // число
console.log(map.get('42')); // строка
console.log(map.get('43')); // undefined
```
