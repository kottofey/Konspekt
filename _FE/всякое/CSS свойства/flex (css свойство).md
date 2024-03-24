Сокращение для `flex-grow`, `flex-shrink` и `flex-basis`
Значнеие по-умолчанию: `flex: 0 1 auto`

Пример:
```css
.flex-item {
  flex: 1 2 300px;
}

/* эквивалентно */

.flex-item {
  flex-grow: 1;
  flex-shrink: 2;
  flex-basis: 300px;
}
```

Также, свойство `flex` может принимать следующие значения: 
```css
{
	flex: initial; -> flex: 0 1 auto;
	flex: auto; -> flex: 1 1 auto;
	flex: none; -> flex: 0 0 auto;
	flex: 1 0; -> flex: 1 0 0%;
	flex: 1; -> flex: 1 1 0%;
}
```
