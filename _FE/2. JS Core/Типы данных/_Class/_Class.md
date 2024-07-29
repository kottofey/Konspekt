```table-of-contents
```

`MyClass` технически является функцией (той, которую мы определяем как `constructor`), в то время как методы, геттеры и сеттеры записываются в `MyClass.prototype`.

Базовый синтаксис для классов выглядит так:

```javascript
class MyClass {
  prop = value; // свойство
  constructor(...) { // конструктор
    // ...
  }
  method(...) {} // метод
  get something(...) {} // геттер
  set something(...) {} // сеттер
  [Symbol.iterator]() {} // метод с вычисляемым именем (здесь - символом)
  // ...
}
```

Затем используйте вызов `new MyClass()` для создания нового объекта со всеми перечисленными методами.

При этом автоматически вызывается метод `constructor()`, в нём мы можем инициализировать объект.

Например:

```javascript
class User {

  constructor(name) {
    this.name = name;
  }

  sayHi() {
    alert(this.name);
  }

}

// Использование:
let user = new User("Иван");
user.sayHi();
```

Когда вызывается `new User("Иван")`:

1. Создаётся новый объект.
2. `constructor` запускается с заданным аргументом и сохраняет его в `this.name`.

Затем можно вызывать на объекте методы, такие как `user.sayHi()`.

> **Методы в классе не разделяются запятой!**

Вот что на самом деле делает конструкция `class User {...}`:

1. Создаёт функцию с именем `User`, которая становится результатом объявления класса. Код функции берётся из метода `constructor` (она будет пустой, если такого метода нет).
2. Сохраняет все методы, такие как `sayHi`, в `User.prototype`.

При вызове метода объекта `new User` он будет взят из прототипа. Таким образом, объекты `new User` имеют доступ к методам класса.

На картинке показан результат объявления `class User`:
![[Pasted image 20240729015517.png]]

# Не просто синтаксический сахар
Иногда говорят, что `class` – это просто «синтаксический сахар» в JavaScript (синтаксис для улучшения читаемости кода, но не делающий ничего принципиально нового), потому что мы можем сделать всё то же самое без конструкции `class`:

```javascript
// перепишем класс User на чистых функциях

// 1. Создаём функцию constructor
function User(name) {
  this.name = name;
}
// каждый прототип функции имеет свойство constructor по умолчанию,
// поэтому нам нет необходимости его создавать

// 2. Добавляем метод в прототип
User.prototype.sayHi = function() {
  alert(this.name);
};

// Использование:
let user = new User("Иван");
user.sayHi();
```

Результат этого кода очень похож. Поэтому, действительно, есть причины, по которым `class` можно считать синтаксическим сахаром для определения конструктора вместе с методами прототипа.

Однако есть важные отличия:

1. Во-первых, функция, созданная с помощью `class`, помечена специальным внутренним свойством `[[IsClassConstructor]]: true`. Поэтому это не совсем то же самое, что создавать её вручную.

В отличие от обычных функций, конструктор класса не может быть вызван без `new`:

```javascript
class User {
  constructor() {}
}

alert(typeof User); // function
User(); // Error: Class constructor User cannot be invoked without 'new'
```

Кроме того, строковое представление конструктора класса в большинстве движков JavaScript начинается с «class …»

```javascript
class User {
  constructor() {}
}

alert(User); // class User { ... }
```

2) Методы класса являются неперечислимыми. Определение класса устанавливает флаг `enumerable` в `false` для всех методов в `"prototype"`.

И это хорошо, так как если мы проходимся циклом `for..in` по объекту, то обычно мы не хотим при этом получать методы класса.

3) Классы всегда используют `use strict`. Весь код внутри класса автоматически находится в строгом режиме.

# Class Expression

Как и функции, классы можно определять внутри другого выражения, передавать, возвращать, присваивать и т.д.

Пример Class Expression (по аналогии с Function Expression):

```javascript
let User = class {
  sayHi() {
    alert("Привет");
  }
};
```

Аналогично Named Function Expression, Class Expression может иметь имя.

Если у Class Expression есть имя, то оно видно только внутри класса:

```javascript
// "Named Class Expression"
// (в спецификации нет такого термина, но происходящее похоже на Named Function Expression)
let User = class MyClass {
  sayHi() {
    alert(MyClass); // имя MyClass видно только внутри класса
  }
};

new User().sayHi(); // работает, выводит определение MyClass

alert(MyClass); // ошибка, имя MyClass не видно за пределами класса
```

Мы даже можем динамически создавать классы «по запросу»:

```javascript
function makeClass(phrase) {
  // объявляем класс и возвращаем его
  return class {
    sayHi() {
      alert(phrase);
    };
  };
}

// Создаём новый класс
let User = makeClass("Привет");

new User().sayHi(); // Привет
```

# Геттеры/сеттеры, другие сокращения

Как и в литеральных объектах, в классах можно объявлять вычисляемые свойства, геттеры/сеттеры и т.д.

Вот пример `user.name`, реализованного с использованием `get/set`:

```javascript
class User {

  constructor(name) {
    // вызывает сеттер
    this.name = name;
  }

  get name() {
    return this._name;
  }

  set name(value) {
    if (value.length < 4) {
      alert("Имя слишком короткое.");
      return;
    }
    this._name = value;
  }

}

let user = new User("Иван");
alert(user.name); // Иван

user = new User(""); // Имя слишком короткое.
```

При объявлении класса геттеры/сеттеры создаются на `User.prototype`, вот так:

```javascript
Object.defineProperties(User.prototype, {
  name: {
    get() {
      return this._name
    },
    set(name) {
      // ...
    }
  }
});
```

Пример с вычисляемым свойством в скобках `[...]`:

```javascript
class User {

  ['say' + 'Hi']() {
    alert("Привет");
  }

}

new User().sayHi();
```

# Свойства классов

В приведённом выше примере у класса `User` были только методы. Давайте добавим свойство:

```javascript
class User {
  name = "Аноним";

  sayHi() {
    alert(`Привет, ${this.name}!`);
  }
}

new User().sayHi();
```

Свойство `name` не устанавливается в `User.prototype`. Вместо этого оно создаётся оператором `new` перед запуском конструктора, это именно свойство объекта.

# Пример создания класса от Владилена

```js
class Animal {
	static type = 'ANIMAL';

	constructior(options) {
		this.name = options.name;
		this.age = options.age;
		this.hasTail = options.hasTail;
	}

	voice() {
		console.log('I am Animal!');
	}
}

const animal = new Animal({
	name: 'Animal Name',
	age: 5,
	hasTail = 'Yes',
})

Animal.type; // ANIMAL
animal.type; // undefined
```

У класса могут быть статические поля, то есть, присущими ТОЛЬКО указанному классу. Обращение может быть только от класса, а не его потомков. 

# Наследование от класса

```js
class Animal {
	static type = 'ANIMAL';

	constructior(options) {
		this.name = options.name;
		this.age = options.age;
		this.hasTail = options.hasTail;
	}

	voice() {
		console.log('I am Animal!');
	}
}

class Cat extends Animal {}
```

Класс `Cat` имеет в прототипе класс `Animal` и все его методы и поля.

Чтобы расширить функциональность дочернего класса, нужно обратиться к конструктору родительского класса при помощи метода `super()`.

# Метод super()
![[super()]]

Можно перезаписывать методы родителя:

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

	voice() {
		console.log('I am Cat!');
	}
}

const cat = new Cat({
	name: 'Cat',
	age: 7,
	hasTail: true,
	color: 'Black'
})
```

Если нужно вызвать метод родителя (например, потому что он был перезаписан). Это можно сделать при помощи `super`:

```js
class Cat extends Animal {
	constructor(options) {
		super(options);
		this.color = "Black";
	}

	voice() {
		console.log('I am Cat!");
	}

	parentVoice() {
		super.voice();
	}
}
```

# Геттеры и сеттеры
![[get(), set()]]

# Примеры!!!

В разметке у нас будет три дива:

```html
// ...
<div id="box1"></div>
<div id="box2"></div>
<div id="circle"></div>
//...
```

Создаем некий компонент, который мы сможем скрывать и показывать методами `show` и `hide`
```js ln=true
class Component {
	constructor(selector) {
		this.$el = document.querySelector("selector");
	}

	hide() {
		this.$el.style.display = 'none';
	}

	show() {
		this.$el.style.display = 'block';
	}
}
```

Далее создаем подкласс компонента - *бокс*. Мы знаем, что конструктор родителя принимает только `selector`. Значит, в конструктор бокса мы передаем опции для конкретного селектора из конструктора родителя. После того как мы вызвали метод `super`, у нас стала доступна переменная `this.$el` и ей можно теперь манипулировать.

```js ln=14
class Box extends Component {
	constructor(options) {
		super(options.selector)

		this.$el.style.width = this.$el.style.height = options.size + 'px';
		this.$el.style.backgroud = options.color;
	}
}

const box1 = new Box({
	selector: '#box1',
	size: 100,
	color: 'red'
})

const box1 = new Box({
	selector: '#box2',
	size: 150,
	color: 'blue'
})
```

Теперь методами `show` и `hide` из родителя можно прятать и показывать элементы, созданные классов `Box`

Идём глубже! Создадим круг от бокса!

```js ln=34
class Circle extends Box {
	constructor(options) {
		super(options);

		this.$el.style.borderRadius = '50%';
	}
}

const c = new Circle({
	selector: '#circle',
	size: 90,
	color: 'green',
})
```

Здесь в конструктор передаем просто `options`, так как в конструктор бокса мы и передавали только `options`