Это сокращение для нескольких свойств фона:
```css
background: [bc] [bi] [br] [bp] [ba];
/* Обозначения:
[bc] — background-color
[bi] — background-image
[br] — background-repeat
[bp] — background-position
[ba] — background-attachment
*/
```

Если какое-то из свойств не указано, то используется свойство по-умолчанию.

```css
background: #e74c3c;
background: url("img.png") no-repeat;
background: url("img.png") 10px 20px;
```

Фоны могут накладываться друг на друга, если они заданы для вложенных друг в друга элементов. Чем глубже элемент — тем выше его фон в стопке.

Можно указывать несколько фонов в одном свойстве, перечислять их через запятую:
```css
background:
  url("img1.png") no-repeat 0 0,
  url("img2.png") repeat-x 50% 50%,
  url("img3.png");
```

Для удобства ширину лучше задавать внешнему элементу (так как все вложенные будут той же ширины), а высоту самому глубокому, так как он растянет по высоте всех своих родителей.

Пример:
```html
<div class="block1">
      <div class="block2">
        <div class="block3"></div>
      </div>   
```

```css
.block1 {
  width: 256px;
  margin: 0 auto;

  background: url("cows.jpg") no-repeat;
  box-shadow: 1px 1px 3px #999999;
}

.block2 {
  background: url("cat_walk.png") no-repeat 190px 195px;
}

.block3 {
  height: 256px;
  background: url("fence.png") no-repeat;
}
```

![[Снимок экрана 2024-03-26 в 01.30.15.png]]
