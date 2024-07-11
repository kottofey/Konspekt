Делает объект из набора пар ключ-значение

```js
// Есть массив ключей-значений:
const array = [[key1, value1], [key2, value2], ..., [keyN, valueN]];

const newObject = Object.fromEntries(array);

// Получится:
{
	key1: value1,
	key2: value2,
	...
	keyN: valueN,
}
```