`Object.setPrototypeOf(obj, proto)`

Сеттер для свойства `[[Prototype]]`. Устанавливает прототип для `obj` на указанный в `proto`

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