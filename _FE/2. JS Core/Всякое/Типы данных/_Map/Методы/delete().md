Удаляем через метод `.delete()`

```js
const map = new Map();

map.set(42, 'число');
map.set('42', 'строка');

map.delete('42');
```