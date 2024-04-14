Ищет элементы по селекторам. Возвращает тег и его содержимое до закрывающего тега, но без этого самого закрывающего тега.
```js
document.querySelector('селектор');
```

```js
// Поиск элемента по тегу
var list = document.querySelector('ul');

// Поиск последнего элемента из списка
var lastProduct = document.querySelector('li:last-child');

// Поиск элемента по классу
var price = document.querySelector('.price');

// Поиск третьего элемента из списка товаров
var thirdProduct = document.querySelector('.product:nth-child(3)');
```

