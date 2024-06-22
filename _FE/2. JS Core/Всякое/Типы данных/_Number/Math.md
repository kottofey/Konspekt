В JavaScript встроен объект [Math](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Math), который содержит различные математические функции и константы.

Примеры:
- `Math.random()`

Возвращает псевдослучайное число в диапазоне от 0 (включительно) до 1 (но не включая 1)

```javascript
alert( Math.random() ); // 0.1234567894322
alert( Math.random() ); // 0.5435252343232
alert( Math.random() ); // ... (любое количество псевдослучайных чисел)
```

- `Math.max(a, b, c...)` / `Math.min(a, b, c...)`

Возвращает наибольшее/наименьшее число из перечисленных аргументов.

```javascript
alert( Math.max(3, 5, -10, 0, 1) ); // 5
alert( Math.min(1, 2) ); // 1
```

- `Math.pow(n, power)`

Возвращает число `n`, возведённое в степень `power`

```javascript
alert( Math.pow(2, 10) ); // 2 в степени 10 = 1024
```

- и т д

