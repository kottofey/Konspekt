Метод `super()` вызывает конструктор родительского класса. В него нужно передать параметры, которые указаны для конструктора дочернего класса, чтобы добавить/расширить поля или методы дочернего класса.

```js
class Animal {
	static type = 'ANIMAL';

	constructor(options) {
		this.name = options.name;
		this.age = options.age;
		this.hasTail = options.hasTail;
	}

	voice() {
		console.log('I am Animal!');
	}
}

class Cat extends Animal {
	constructor(options) {
		super(options);
		this.color = "Black";
	}
}

const cat = new Cat({
	name: 'Cat',
	age: 7,
	hasTail: true,
	color: 'Black'
})
```