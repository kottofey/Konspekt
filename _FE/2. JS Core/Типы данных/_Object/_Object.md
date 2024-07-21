```table-of-contents
```

```js
const user = {
	firstName: 'Roman',
	age: 30,
	isAdmin: true,
	email: 'email@server.com',
	'user-address': {
		city: 'Moscow',
		street: 'StrretName'
	},
	skills: ['html', 'css', 'js'],
}
```

Состоит из `свойств`, которые представляют собой пары ключей и значений. Значения могут быть любым другим типом данных, например, другие вложенные объекты, [[массивы]] и т д.

Ключи должны оборачиваться кавычками, если состоят из чего-то большего, чем просто набор букв. Например, если ключ включает в себя дефис. Без кавычек он будет восприниматься, как знак вычитания.

#### Флаги свойств

Помимо значения **`value`**, свойства объекта имеют три специальных атрибута (так называемые «флаги»).

- **`writable`** – если `true`, свойство можно изменить, иначе оно только для чтения.
- **`enumerable`** – если `true`, свойство перечисляется в циклах, в противном случае циклы его игнорируют.
- **`configurable`** – если `true`, свойство можно удалить, а эти атрибуты можно изменять, иначе этого делать нельзя.

Метод [Object.getOwnPropertyDescriptor](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptor) позволяет получить _полную_ информацию о свойстве.

Его синтаксис:

```javascript
let descriptor = Object.getOwnPropertyDescriptor(obj, propertyName);
```

`obj`

Объект, из которого мы получаем информацию.

`propertyName`

Имя свойства.

Возвращаемое значение – это объект, так называемый «дескриптор свойства»: он содержит значение свойства и все его флаги.

Например:

```javascript
let user = {
  name: "John"
};

let descriptor = Object.getOwnPropertyDescriptor(user, 'name');

alert( JSON.stringify(descriptor, null, 2 ) );
/* дескриптор свойства:
{
  "value": "John",
  "writable": true,
  "enumerable": true,
  "configurable": true
}
*/
```

Чтобы изменить флаги, мы можем использовать метод [Object.defineProperty](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty).

Его синтаксис:

```javascript
Object.defineProperty(obj, propertyName, descriptor)
```

`obj`, `propertyName`

Объект и его свойство, для которого нужно применить дескриптор.

`descriptor`

Применяемый дескриптор.

Если свойство существует, `defineProperty` обновит его флаги. В противном случае метод создаёт новое свойство с указанным значением и флагами; если какой-либо флаг не указан явно, ему присваивается значение `false`.

Например, здесь создаётся свойство `name`, все флаги которого имеют значение `false`:

```javascript
let user = {};

Object.defineProperty(user, "name", {
  value: "John"
});

let descriptor = Object.getOwnPropertyDescriptor(user, 'name');

alert( JSON.stringify(descriptor, null, 2 ) );
/*
{
  "value": "John",
  "writable": false,
  "enumerable": false,
  "configurable": false
}
 */
```

Сравните это с предыдущим примером, в котором мы создали свойство `user.name` «обычным способом»: в этот раз все флаги имеют значение `false`. Если это не то, что нам нужно, надо присвоить им значения `true` в параметре `descriptor`.

##### Только для чтения (writable: false)

Сделаем свойство `user.name` доступным только для чтения. Для этого изменим флаг `writable`:

```javascript
let user = {
  name: "John"
};

Object.defineProperty(user, "name", {
  writable: false
});

user.name = "Pete"; // Ошибка: Невозможно изменить доступное только для чтения свойство 'name'
```

Теперь никто не сможет изменить имя пользователя, если только не обновит соответствующий флаг новым вызовом `defineProperty`.

Ошибки появляются только в строгом режиме

В нестрогом режиме, без `use strict`, мы не увидим никаких ошибок при записи в свойства «только для чтения» и т.п. Но эти операции всё равно не будут выполнены успешно. Действия, нарушающие ограничения флагов, в нестрогом режиме просто молча игнорируются.

Вот тот же пример, но свойство создано «с нуля»:

```javascript
let user = { };

Object.defineProperty(user, "name", {
  value: "John",
  // для нового свойства необходимо явно указывать все флаги, для которых значение true
  enumerable: true,
  configurable: true
});

alert(user.name); // John
user.name = "Pete"; // Ошибка
```

##### Неперечислимое свойство (enumerable: false)

Добавим собственный метод `toString` к объекту `user`.

Встроенный метод `toString` в объектах – неперечислимый, его не видно в цикле `for..in`. Но если мы напишем свой собственный метод `toString`, цикл `for..in` будет выводить его по умолчанию:

```javascript
let user = {
  name: "John",
  toString() {
    return this.name;
  }
};

// По умолчанию оба свойства выведутся:
for (let key in user) alert(key); // name, toString
```

Если мы этого не хотим, можно установить для свойства `enumerable:false`. Тогда оно перестанет появляться в цикле `for..in` аналогично встроенному `toString`:

```javascript
let user = {
  name: "John",
  toString() {
    return this.name;
  }
};

Object.defineProperty(user, "toString", {
  enumerable: false
});

// Теперь наше свойство toString пропало из цикла:
for (let key in user) alert(key); // name
```

Неперечислимые свойства также не возвращаются `Object.keys`:

```javascript
alert(Object.keys(user)); // name
```

##### Неконфигурируемое свойство (configurable: false)

Флаг неконфигурируемого свойства (`configurable:false`) иногда предустановлен для некоторых встроенных объектов и свойств.

Неконфигурируемое свойство не может быть удалено, его атрибуты не могут быть изменены.

Например, свойство `Math.PI` – только для чтения, неперечислимое и неконфигурируемое:

```javascript
let descriptor = Object.getOwnPropertyDescriptor(Math, 'PI');

alert( JSON.stringify(descriptor, null, 2 ) );
/*
{
  "value": 3.141592653589793,
  "writable": false,
  "enumerable": false,
  "configurable": false
}
*/
```

То есть программист не сможет изменить значение `Math.PI` или перезаписать его.

```javascript
Math.PI = 3; // Ошибка, потому что writable: false

// delete Math.PI тоже не сработает
```

Мы также не можем изменить `writable`:

```javascript
// Ошибка, из-за configurable: false
Object.defineProperty(Math, "PI", { writable: true });
```

Мы абсолютно ничего не можем сделать с `Math.PI`.

Определение свойства как неконфигурируемого – это дорога в один конец. Мы не можем изменить его обратно с помощью `defineProperty`.

**Обратите внимание: `configurable: false` не даст изменить флаги свойства, а также не даст его удалить. При этом можно изменить значение свойства.**

В коде ниже свойство `user.name` является неконфигурируемым, но мы все ещё можем изменить его значение (т.к. `writable: true`).

```javascript
let user = {
  name: "John"
};

Object.defineProperty(user, "name", {
  configurable: false
});

user.name = "Pete"; // работает
delete user.name; // Ошибка
```

А здесь мы делаем `user.name` «навечно запечатанной» константой, как и встроенный `Math.PI`:

```javascript
let user = {
  name: "John"
};

Object.defineProperty(user, "name", {
  writable: false,
  configurable: false
});

// теперь невозможно изменить user.name или его флаги
// всё это не будет работать:
user.name = "Pete";
delete user.name;
Object.defineProperty(user, "name", { value: "Pete" });
```

##### Метод Object.defineProperties()

![[Object.defineProperties()]]

##### Метод Object.getOwnPropertyDescriptors()

![[Object.getOwnPropertyDescriptors()]]

##### Глобальное запечатывание объекта

Дескрипторы свойств работают на уровне конкретных свойств.

Но ещё есть методы, которые ограничивают доступ ко _всему_ объекту:

![[Object.preventExtensions()]]

Запрещает добавлять новые свойства в объект.

![[Object.seal()]]

Запрещает добавлять/удалять свойства. Устанавливает `configurable: false` для всех существующих свойств.

![[Object.freeze()]]

Запрещает добавлять/удалять/изменять свойства. Устанавливает `configurable: false, writable: false` для всех существующих свойств.

А также есть методы для их проверки:

![[Object.isExtensible()]]

Возвращает `false`, если добавление свойств запрещено, иначе `true`.

![[Object.isSealed()]]
Возвращает `true`, если добавление/удаление свойств запрещено и для всех существующих свойств установлено `configurable: false`.

![[Object.isFrozen()]]

Возвращает `true`, если добавление/удаление/изменение свойств запрещено, и для всех текущих свойств установлено `configurable: false, writable: false`.

На практике эти методы используют редко.
#### Доступ к свойствам объекта

Можно полчить доступлибо через точку: `user.firstName`
Либо через квадратные скобки: `user['isAdmin']`, `user['user-address']`
> Доступ к сложным ключам можно получить только через квадратные скобки.

Чтобы получить доступ ко вложенным свойствам, можно продолжить цепочку:
- `user['user-address'].city`
- `user['user-address'].['city']`
- `user['skills'][0]` - выдаст 'html'

- `user['user-address'].[city]` - даст ошибку, интерпретатор посчитает `city` за переменную и пожалуется, что она не определена

#### Изменение свойств
`user.firstName = 'OtherName'`

Если присвоить объекту поле, которого в нём нет, такое поле создастся.

Если попытаться записать или обратиться к свойству свойства, которого не существует, то будет ошибка.

```js
const obj = {
	key1: {
	subkey1: value
	},
}

obj.key2.subkey2 = 'smth'; // ОШИБКА!
```

Мы создаем свойство `key2`, которое будет иметь значение `undefined`, а у `undefined` невозможно создать свои свойства. Нужно сначала инициализировать внутренний объект, хотя бы пустым объектом `{}` и тогда у него можно будет создавать свойства.
#### Другие типы объектов
Подтипами объектов являются также:
- [[Массивы]]
- Функции
- Даты `new Date()`

#### Использование оператора `new`
```js
// Все функции-конструкторы, созданные с помощью 'new', будут иметь тип 'object'
var str = new String("String");
var num = new Number(100);

typeof str; // Вернёт 'object'
typeof num; // Вернёт 'object'

// Но существует исключение для конструктора Function

var func = new Function();

typeof func; // Вернёт 'function'
```

#### Методы и функции
![[hasOwnProperty(prop)]]

![[Object.is()]]