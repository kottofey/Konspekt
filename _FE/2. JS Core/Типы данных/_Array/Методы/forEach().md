Принимает коллбэк в котором будут аргументы: `элемент масива`, `индекс`, `сам массив`

```js
users.forEach(currentValue[, index[, array]]) => {
	// ...
});
```

Можно указать только элемент, индекс и массив необязательны

# Контекст в forEach()
Вторым необязательным параметром `forEach` принимает контекст. Если его не передать, то `this` будет равен `undefined`.

```js ln=true
const obj = {
	lastName: 'Ivanov',
	firstNames: ['Petr', 'Ivan'],
	logFullNames: function() {
		this.firstNames.forEach(function(name) {
			console.log(`${this.lastName} ${name}`);
		})
	},
	logFullNames1: function() {
		this.firstNames.forEach( (name) => {
			console.log(`${this.lastName} ${name}`);
		})
	},
	logFullNames2: function() {
		this.firstNames.forEach(function(name) {
			console.log(`${this.lastName} ${name}`);
		}, this)
	},
}

obj.logFullNames(); // undefined Petr, undefined Ivan
obj.logFullNames1(); // Ivanov Petr, Ivanov Ivan
obj.logFullNames2(); // Ivanov Petr, Ivanov Ivan
```

Здесь `logFullNames` вызывает `forEach`, который использует коллбэк-функцию, которая создает свой собственный контекст. И `this` внутри коллбэка не будет иметь свойств `lastName`, а потому и будет выведен undefined

`logFullNames1` использует стрелочную функцию, которая не имеет своего контекста и использует родительский контекст. А потому выведет всё правильно.

Можно исправить ситуацию с `logFullNames`, в `logFullNames2` передав в `forEach` контекст в качестве второй переменной. Тогда всё будет работать!