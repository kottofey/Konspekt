Метод [toFixed(n)](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed) округляет число до `n` знаков после запятой и возвращает строковое представление результата.

```javascript
let num = 12.34;
alert( num.toFixed(1) ); // "12.3"
```

Округляет значение до ближайшего числа, как в большую, так и в меньшую сторону, аналогично методу `Math.round`:

```javascript
let num = 12.36;
alert( num.toFixed(1) ); // "12.4"
```

Обратите внимание, что результатом `toFixed` является строка. Если десятичная часть короче, чем необходима, будут добавлены нули в конец строки:

```javascript
let num = 12.34;
alert( num.toFixed(5) ); // "12.34000", добавлены нули, чтобы получить 5 знаков после запятой
```

Мы можем преобразовать полученное значение в число, используя унарный оператор `+` или `Number()`, пример с унарным оператором: `+num.toFixed(5)`.