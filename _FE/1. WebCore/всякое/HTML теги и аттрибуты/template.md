Было бы удобно, если бы вся необходимая разметка для будущих элементов уже где-то хранилась. Нам бы оставалось только подправить содержимое под каждый элемент. И это можно сделать с помощью тега `template`.

Он хранит в себе шаблон для будущих элементов. Тег `template` находится там же, где и вся разметка сайта, только его содержимое не отображается на странице. В нашей разметке тоже есть `template`. Он хранит шаблонную разметку новой задачи.

> ==\ Важный момент!\ == Созданный через темплейт элемент уникален! Его можно будет использовать только один раз! Чтобы можно было его копировать его нужно, неожиданно, но скопировать, а точнее, склонировать. Что можно сделать с помощью метода [[cloneNode()]]

Чтобы получить `template` в JavaScript, его можно найти по названию тега, например, через `querySelector('template')`. У этого способа есть минус — шаблонов на странице может быть много. Обычно каждому тегу `template` дают уникальное название и записывают в атрибут `id` (идентификатор). Значения этого атрибута не могут повторяться на одной странице. По `id` можно найти необходимый шаблон.

Шаблон в разметке:
```html
<body>
  <template id="text-template">
		<li class="todo-list-item">  
		    <label>  
		      <input type="checkbox" class="todo-list-input"/>  
		      <span></span>
		    </label>  
		  </li>
  </template>
</body>
```

Поиск элемента в JavaScript:
```js
document.querySelector('#text-template');
```

Если развернуть содержимое темплейта в консоли, можно увидеть, что внутри него есть некий `document-fragment`, а уже внутри него тот самый шаблон, который нам нужен.

``` title="Вывод в консоль элемента:"
-> #document-fragment (DocumentFragment)  
  <li class="todo-list-item">  
    <label>  
      <input type="checkbox" class="todo-list-input"/>  
      <span>  
    </label>  
  </li>
```

Что это за `document-fragment` и как из него достать наш шаблон?

`document-fragment` или просто фрагмент является хранилищем содержимого тега `template`. Именно благодаря ему разметка из `template` не отображается на странице. Вы можете в этом убедиться, если добавите самому тегу стили: например, явную ширину и высоту и яркий фоновый цвет. Тогда вы увидите элемент `template` на странице, но его содержимое нет.

Если искать элементы через `querySelector` и другие методы поиска внутри `template`, то мы не получим нужные нам элементы. Они лежат в свойстве `content` этого тега. Это свойство и содержит в себе `document-fragment`, внутри которого уже можно искать привычными методами поиска.

```html
<body>
  …
  <template id="text-template">
    <p class="text"></p>
  </template>
</body>
```

Если мы хотим найти элемент в шаблоне, надо искать так:

```js
var template = document.querySelector('#text-template');
// Нашли template в документе

var content = template.content;
// Получили содержимое, фрагмент

var text = content.querySelector('.text');
// Нашли нужный шаблон внутри содержимого темплейта
```

Эту запись можно сократить. Например, записать в отдельную переменную контент, а в другую искомый шаблон.

```js
var textTemplate = document.querySelector('#text-template').content;
var text = textTemplate.querySelector('.text');
```

Такая запись удобней, потому что отдельно в коде элемент `template` обычно не используют. Вся работа ведётся с его контентом и шаблоном, который в этом контенте хранится.

В шаблоне можно менять текст, классы, а затем добавлять элементы на страницу.

