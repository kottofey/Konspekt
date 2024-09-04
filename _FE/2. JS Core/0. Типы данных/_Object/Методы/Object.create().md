`Object.create(proto[, descriptors])`

Создаёт пустой объект со свойством `[[Prototype]]`, указанным как `proto`, и необязательными дескрипторами свойств `descriptors`

```javascript
let animal = {
  eats: true
};

// создаём новый объект с прототипом animal
let rabbit = Object.create(animal);

alert(rabbit.eats); // true
```

У `Object.create` есть необязательный второй аргумент: дескрипторы свойств. Мы можем добавить дополнительное свойство новому объекту таким образом:

```javascript
let animal = {
  eats: true
};

let rabbit = Object.create(animal, {
  jumps: {
    value: true
  }
});

alert(rabbit.jumps); // true
```

Мы также можем использовать `Object.create` для «продвинутого» клонирования объекта, более мощного, чем копирование свойств в цикле `for..in`:

```javascript
// клон obj c тем же прототипом (с поверхностным копированием свойств)
let clone = Object.create(Object.getPrototypeOf(obj), Object.getOwnPropertyDescriptors(obj));
```

Такой вызов создаёт точную копию объекта `obj`, включая все свойства: перечисляемые и неперечисляемые, геттеры/сеттеры для свойств – и всё это с правильным свойством `[[Prototype]]`.

# Дескрипторы

При создании объекта, при описании свойств можно указывать дескрипторы:

- [[_Object#Неперечислимое свойство (enumerable false)|enumerable]]
- [[_Object#Только для чтения (writable false)]|writable]]
- [[_Object#Неконфигурируемое свойство (configurable false)|configurable]]

```js
const person = Object.create(
	{},
	{
		name: {
			value: 'Roman',
			enumerable: true,
			writable: true,
			configurable: true 
		}
	}
)

for (let key in person) {
	console.log(key, person[key]);
} // name Roman
```

Если дескрипторы не указать, то по-умолчанию они все равняются `false`

