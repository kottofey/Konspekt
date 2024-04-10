Делает преобразования плавными

```css
transition: property duration timing-function delay;
```

- `property` — определяет CSS-свойство, для которого будет применяться переход. Можно указать несколько свойств, разделив их запятой. Если указать `all`, переходы будут применяться ко всем свойствам элемента. Отдельно задается свойством [transition-property](transition-property.md)
- `duration` — определяет длительность перехода. Задаётся в секундах `s` или миллисекундах `ms`. Отдельно задается свойством [transition-duration](transition-duration.md)
- `timing-function` — определяет скорость перехода в разные моменты времени. Наиболее часто используются следующие функции: `linear`, `ease`, `ease-in`, `ease-out`, `ease-in-out`. Отдельно задается свойством [transition-timing-function](transition-timing-function.md)
- `delay` — время задержки перед началом перехода. Задаётся в секундах `s` или миллисекундах `ms`. Отдельно задается свойством [transition-delay](transition-delay.md)

В примере цвет фона плавно поменяется при наведении за 1 секунду
```css
p {
  background-color: blue;
  transition: background-color 1s ease-in-out;
}

p:hover {
  background-color: red;
}
```

А здесь высота и ширина плавно изменятся при наведении. Можно описывать изменения нескольких свойств через запятую.
```css
p {
  width: 100px;
  height: 100px;
  transition: width 2s, height 4s;
}

p:hover {
  width: 200px;
  height: 200px;
}
```

Не все свойства возможно анимировать. Для корректной работы перехода изменяемое свойство должно быть анимируемым. Например:

- Цветовые свойства: color, background-color, border-color и другие.
- Размеры и отступы: width, height, padding, margin, top, right, bottom, left и другие.
- Свойства трансформации: transform (включая rotate, scale, translate, skew и другие).
- Некоторые свойства текста: font-size, letter-spacing, word-spacing, line-height.
- Свойство прозрачности: opacity.
- Свойства границы: border-width, border-radius.
- Свойство позиционирования: position.