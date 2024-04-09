**`Element.classList`** — это доступное только для чтения свойство, которое содержит текущую коллекцию [`DOMTokenList`](https://developer.mozilla.org/ru/docs/Web/API/DOMTokenList) всех атрибутов `class` элемента.

Хоть оно и доступно только для чтения, его элементы можно менять при помощи методов:
- add()
- remove()
- replace()
- toggle()

**Примеры**
Добавляем элементу новый класс:
```js
element.classList.add("some-new-class");
```

Ищем в списке классов элемента (в списке classList) нужный старый класс и удаляем его:
```js
element.classList.remove("some-old-class");
```

