Этот метод принимает на вход элемент и вставляет его в **конец** родительского элемента. То есть, если в списке уже есть три элемента, добавленный с помощью `appendChild` элемент станет четвёртым в списке.

```js
var list = document.querySelector('.cards');
var card = document.createElement('li');
card.classList.add('card');

// После вызова этого метода новый элемент отрисуется на странице
list.appendChild(card);
```

Вот что произойдёт с разметкой после вызова `appendChild`:
```js
<!-- Исходное состояние разметки -->
<ul class="cards">
  <li class="card">Существующий элемент</li>
</ul>

<!-- Состояние после вызова appendChild -->
<ul class="cards">
  <li class="card">Существующий элемент</li>
  <li class="card">Добавленный элемент</li>
</ul>
```

