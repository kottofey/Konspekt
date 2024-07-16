Проверяет на наличие элемента в множестве

```js
set.add('button')
	.add('active')
	.add('active');
	
console.log(set.has('active')); // true
console.log(set.has('primary')); // false
```

С проверкой на объекты есть нюанс, так как передаются ссылки на объекты. Поэтому получится следующая ситуация:

```js ln=true
const set = new Set();

set.add({ className: 'button' });

console.log(set.has({ className: 'button' })); // false
```

Объекты не равны, так как на строке `3` и `5` передаются разные объекты, хоть они по содержимому и одинаковые. Решить эту проблему можно запис ав объект в переменную, которая будет хрангить ссылку на него. И уже переменную нужно передавать в значение множества и сравнивать со ссылкой.

```js ln=true
const set = new Set();
const buttonRef = { className: 'button' };
set.add(buttonRef);

console.log(set.has(buttonRef)); // true
```

