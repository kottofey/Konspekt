Чтобы получить все дескрипторы свойств сразу, можно воспользоваться методом [Object.getOwnPropertyDescriptors(obj)](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptors).

Вместе с `Object.defineProperties` этот метод можно использовать для клонирования объекта вместе с его флагами:

```javascript
let clone = Object.defineProperties({}, Object.getOwnPropertyDescriptors(obj));
```

Обычно при клонировании объекта мы используем присваивание, чтобы скопировать его свойства:

```javascript
for (let key in user) {
  clone[key] = user[key]
}
```

…Но это не копирует флаги. Так что если нам нужен клон «получше», предпочтительнее использовать `Object.defineProperties`.

Другое отличие в том, что `for..in` игнорирует символьные и неперечислимые свойства, а `Object.getOwnPropertyDescriptors` возвращает дескрипторы _всех_ свойств.