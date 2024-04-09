Позволяет получить текстовое содержимое элемента.

```html
<p>Я текст!</p>
```

```js
let paragraph = document.querySelector("p");
console.log(paragraph.textContent);
```

Этот скрипт выведет в консоль "Я текст!"
То есть, берется только содержимое между тегами.

Его можно менять просто присвоив ему новое значение.

```js
paragraph = "New wonderful text!"
```

Оно не поймет html кода, то есть, сделать вот так не получится:
```js
paragraph = "New wonderful and <b>BOLD</b> text!"
```
