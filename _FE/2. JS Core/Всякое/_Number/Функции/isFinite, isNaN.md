- `Infinity` (и `-Infinity`) — особенное численное значение, которое ведёт себя в точности как математическая бесконечность ∞.
- `NaN` представляет ошибку.

Эти числовые значения принадлежат типу `number`, но они не являются «обычными» числами, поэтому есть функции для их проверки:

- `isNaN(value)` преобразует значение в число и проверяет является ли оно `NaN`:
  
```javascript
alert( isNaN(NaN) ); // true
alert( isNaN("str") ); // true
```

Нужна ли нам эта функция? Разве не можем ли мы просто сравнить `=== NaN`? К сожалению, нет. Значение `NaN` уникально тем, что оно не является равным ничему другому, даже самому себе:

```javascript
alert( NaN === NaN ); // false
```

- `isFinite(value)` преобразует аргумент в число и возвращает `true`, если оно является обычным числом, т.е. не `NaN/Infinity/-Infinity`:
    
```javascript
alert( isFinite("15") ); // true
alert( isFinite("str") ); // false, потому что специальное значение: NaN
alert( isFinite(Infinity) ); // false, потому что специальное значение: Infinity
```

Иногда `isFinite` используется для проверки, содержится ли в строке число:

```javascript
let num = +prompt("Введите число:", '');

// вернёт true всегда, кроме ситуаций, когда аргумент - Infinity/-Infinity или не число
alert( isFinite(num) );
```

Помните, что пустая строка интерпретируется как `0` во всех числовых функциях, включая`isFinite`.

## Number.isNaN() и Number.isFinite()
Методы [Number.isNaN](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Number/isNaN) и [Number.isFinite](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Number/isNaN) – это более «строгие» версии функций `isNaN` и `isFinite`. Они не преобразуют аргумент в число, а наоборот – первым делом проверяют, является ли аргумент числом (принадлежит ли он к типу `number`).

- `Number.isNaN(value)` возвращает `true` только в том случае, если аргумент принадлежит к типу `number` и является `NaN`. Во всех остальных случаях возвращает `false`.
 
 ```javascript
alert( Number.isNaN(NaN) ); // true
alert( Number.isNaN("str" / 2) ); // true

// Обратите внимание на разный результат:
alert( Number.isNaN("str") ); // false, так как "str" является строкой, а не числом
alert( isNaN("str") ); // true, так как isNaN сначала преобразует строку "str" в число и в результате преобразования получает NaN
```

- `Number.isFinite(value)` возвращает `true` только в том случае, если аргумент принадлежит к типу `number` и не является `NaN/Infinity/-Infinity`. Во всех остальных случаях возвращает `false`.
 
```javascript
alert( Number.isFinite(123) ); // true
alert( Number.isFinite(Infinity) ); // false
alert( Number.isFinite(2 / 0) ); // false

// Обратите внимание на разный результат:
alert( Number.isFinite("123") ); // false, так как "123" является строкой, а не числом
alert( isFinite("123") ); // true, так как isFinite сначала преобразует строку "123" в число 123
```

Не стоит считать `Number.isNaN` и `Number.isFinite` более «корректными» версиями функций `isNaN` и `isFinite`. Это дополняющие друг-друга инструменты для разных задач.