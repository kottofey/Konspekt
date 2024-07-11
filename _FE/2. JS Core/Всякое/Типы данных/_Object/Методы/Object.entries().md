Возвращает массив массивов, где каждый элемент является парой ключ-значение

```js
const obj = {
	key1: value1,
	key2: value2,
	...
	keyN: valueN,
}

const entries = Object.entries(obj);

// результат
[[key1, value1], [key2, value2]...[keyN, valueN]]
```

