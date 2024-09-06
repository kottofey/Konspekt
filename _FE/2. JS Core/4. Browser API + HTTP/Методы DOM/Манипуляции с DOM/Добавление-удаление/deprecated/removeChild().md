`parentElem.removeChild(node)`

Удаляет `node` из `parentElem` (предполагается, что он родитель `node`).

Этот пример удалит первый `<li>` из `<ol>`:

```html
<ol id="list">
  <li>0</li>
  <li>1</li>
  <li>2</li>
</ol>

<script>
  let li = list.firstElementChild;
  list.removeChild(li);
</script>
```

Все эти методы возвращают вставленный/удалённый узел. Другими словами, `parentElem.appendChild(node)` вернёт `node`. Но обычно возвращаемое значение не используют, просто вызывают метод.