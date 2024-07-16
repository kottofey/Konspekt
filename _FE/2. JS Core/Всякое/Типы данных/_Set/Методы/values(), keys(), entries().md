### Методы .keys(), .values()

Так как у множества нет понятия "ключ", то метод `.keys()` будет работать также, как и `.values()`. Оба они возвращают перебираемый объект `SetIterator`

```js
set.add('button')
	.add('active')
	.add('active');

console.log(set.values()); // SetIterator { 'button', 'active' }

console.log(set.keys()); // SetIterator { 'button', 'active' }
```

Чтобы получить сами элементы используем spread

```js
set.add('button')
	.add('active')
	.add('active');

console.log(...set.values()); // [ 'button', 'active' ]
```

### Метод .entries()
Так как у множества нет понятия ключ-значение, метод `.entries()` вернет массив массивов, где будут пары одинаковых значений на местах ключа и значения.

```js
set.add('button')
	.add('active')
	.add('active');

console.log(...set.entries()); // [ 'button', 'button' ], [ 'active', 'active' ]
```