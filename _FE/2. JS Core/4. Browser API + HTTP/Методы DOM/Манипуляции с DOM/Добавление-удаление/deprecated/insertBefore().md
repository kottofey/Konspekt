`parentElem.insertBefore(node, nextSibling)`

Вставляет `node` перед `nextSibling` в `parentElem`.

Следующий пример вставляет новый элемент перед вторым `<li>`:

```html
<ol id="list">
  <li>0</li>
  <li>1</li>
  <li>2</li>
</ol>
<script>
  let newLi = document.createElement('li');
  newLi.innerHTML = 'Привет, мир!';

  list.insertBefore(newLi, list.children[1]);
</script>
```

Чтобы вставить `newLi` в начало, мы можем сделать вот так:

```javascript
list.insertBefore(newLi, list.firstChild);
```