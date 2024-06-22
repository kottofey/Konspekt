```js
switch(key) {
	case: 'value1':
		actions1;
		break;
	case: 'value2':
		actions2;
		break;
	default:
		defaultActions;
}
```

Если не указать `break`, то при совпадении кейса действие выполнится и уйдёт на следующее сравнение. `break` прерывает сравнение и выходит из кейса. 

Можно склеивать условия, будет работать как логическое `ИЛИ`:

```js
switch(color) {
	case 'yellow':
	case 'red':
		console.log('yellow or red');
		break;
	default:
		someDefaultActions;
}
```
