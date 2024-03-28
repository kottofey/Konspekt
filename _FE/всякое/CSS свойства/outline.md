Это обводка! Очень похожа на `border`, но обводка не принимает участия в блочной модели и рисуется за внешней границей рамки по границе контента. На картинке обводка черная, а рамка красная.

```css 
div {
  width: 420px;
  height: 200px;
  background: #eee;
  font-size: 150px;
  outline: 10px solid black;
  border: 20px solid red;
}
```

![[1.webp]]

Обводка не занимает места, если друг за другом расположить два блока, то обводки наложатся. ![[2.webp]]

Обводка одинакова со всех сторон, в то время, как рамке можно задать индивидуальное значение для каждой стороны. 

```css
div {
  outline: 10px solid black;
  border-width: 20px;
  border-style: solid;
  border-top-color: red;
  border-left-color: green;
  border-right-color: blue;
  border-bottom-color: orange;
}
```
![[3.webp]]

Если обводке не задать толщину через `outline-width`, то оно примет значение, как если бы обводки не было. Обычно это 3 пикселя на десктопных браузерах.

```css
div {
  outline: solid;
  border: 20px solid red;
}
```
![[4.webp]]

По-умолчанию обводка прямоугольная. Она повторяет форму границы и её можно регулировать через `border-radius`.
```css
div {
  outline: 10px solid black;
  border: 20px solid red;
  border-radius: 50px;
}
```
![[5.webp]]

