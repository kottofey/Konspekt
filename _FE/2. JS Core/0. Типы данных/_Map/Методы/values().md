```js ln=true
const map = new Map();

map.set(1, 'one')
	.set(2, 'two')
	.set(3, 'three');

console.log(map.values());
// MapIterator { }

console.log([...map.values]);
// ['one', 'two', 'three']
```

Возвращает объект `MapIterator`, это объект для перебора.

Можно сконвертировать это в массив через `spread` и обернув в квадратные скобки (строка `10`). `Spread` выдаст значения по порядку, а скобки превратят их в массив.
