Эти свойства служат для управления сорсом и альтернативным содержанием картинки. Например, [[Финты#Упрощение создания элементов|функцией]] для создания мы создаём картинку и свойствами `src` и `alt` передаем ей путь и задаем значение альту:
```js
let imageElement = createElement('img', 'some__image');
imageElement.src = 'images/some_image.jpg';
imageElement.alt = 'image alternative text';
```
