Добавляет элементы в множество

```js
const set = new Set();

set.add('button');

console.log(set); // button

set.add('active');

console.log(set); // button, active

set.add('active');

console.log(set); // button, active
// всё еще два элемента, т.к. уже есть один active
```

Можно вызывать метод `add()` по цепочке и добавлять элементы подряд.

```js
set.add('button')
	.add('active')
	.add('active');
	
console.log(set); // button, active
```