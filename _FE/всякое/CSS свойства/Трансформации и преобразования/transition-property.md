Указывает свойство, которое нужно плавно изменять. По умолчанию оно равно `all`, что будет менять ВСЕ свойства элемента. Часто такое поведение не желательно.

```css
transition-property: width;     // плавно меняется только ширина
transition-property: width, height; // плавно меняются ширина и высота
```

```css
transition-property: width, height;
transition-duration: 1s, 5s; // ширина меняется за 1 секунду, высота за 5
```
