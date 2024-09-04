Создает новый массив из того, что вернул коллбэк для каждого из элементов массива.

```js
const new_array = arr.map(function callback( currentValue[, index[, array]] ) {
    // Возвращает элемент для new_array
}[, thisArg])
```

Параметры:

- `callback`
	Функция, вызываемая для каждого элемента массива arr. Каждый раз, когда callback выполняется, возвращаемое значение добавляется в new_array.

Функция `callback`, создающая элемент в новом массиве, принимает три аргумента:

- `currentValue`
	Текущий обрабатываемый элемент массива.
	
- `index` (Необязательный)
	Индекс текущего обрабатываемого элемента в массиве.
	
- `array` (Необязательный)
	Массив, по которому осуществляется проход.

- `thisArg` (Необязательный)
	Значение, используемое в качестве this при вызове функции callback


```js
const usersName = users.map(user => user.name);
console.log(usersName);

// или //

const usersNameAge = users.map( user => ({name: user.name, age: user.age}) );
console.log(usersNameAge);
```
