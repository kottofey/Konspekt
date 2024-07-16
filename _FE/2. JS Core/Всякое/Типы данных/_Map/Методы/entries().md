Возвращает массив массивов со значениями ключ-значение мапы

```js ln=true
const map = new Map();

map.set(1, 'one')
	.set(2, 'two')
	.set(3, 'three');

console.log(map.entries());
// MapIterator { }

console.log([...map.entries]);
/*
[
	[ 1, "one" ],
	[ 2, "two" ],
	[ 3, "three" ]
]
*/
```

Метод `entries()` можно использовать доля клонирования мапы.

```js
const map = new Map();

map.set(1, 'one')
	.set(2, 'two')
	.set(3, 'three');

const map2 = new Map(map.entries());

const [ [key, value], second, third] ] = map;

console.log(key, value); // 1, one
```