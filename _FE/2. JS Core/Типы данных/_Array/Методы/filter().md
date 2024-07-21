Создает новый массив, обосновываясь на результате коллбэка. Если коллбэк вернет `true`, то элемент попадет в новый массив. Если `false`, то не попадёт.

```js
const userLess30 = users.filter(user => user.age < 30);
console.log(userLess30);
```
