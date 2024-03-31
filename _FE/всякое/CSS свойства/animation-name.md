Название анимации указывается в `@keyframes`, а `animation-name` задаёт элементу анимацию, которую нужно проиграть.

```css
@keyframes smth {  
  50% {  
   transform: rotate(180deg);  
  }
}

.block-name {
	animation-name: smth;
}
```
