`Object.getPrototypeOf(obj)`

Геттер для свойства `[[Prototype]]`

Возвращает прототип для указанного объекта.

```javascript
let animal = {
  eats: true
};

// создаём новый объект с прототипом animal
let rabbit = Object.create(animal);

alert(rabbit.eats); // true

alert(Object.getPrototypeOf(rabbit) === animal); // получаем прототип объекта rabbit

Object.setPrototypeOf(rabbit, {}); // заменяем прототип объекта rabbit на {}
```

