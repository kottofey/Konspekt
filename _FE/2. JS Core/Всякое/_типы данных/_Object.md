```js
let object = {
	key: value,
}
// значения могут быть любым другим типом данных
```

Подтипами объектов являются также:
- Массивы
- Функции
- Даты `new Date()`

## Использование оператора `new`
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

