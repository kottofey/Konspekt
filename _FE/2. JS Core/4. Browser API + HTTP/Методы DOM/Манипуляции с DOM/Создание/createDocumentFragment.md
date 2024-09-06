В этот метод ничего не передается. Это такой же DOM узел в который можно добавлять элементы и выполнять все манипу4ляции. Когда он добавляется в документ он исчезает, выполнив свою работу. Обратиться к нему после добавления уже нельзя. 

```js
const fragment = documentCreateFragment();
const colors = ['black', 'yellow', 'orange'];

colors.forEach( color => {
	const item = document.createElement('div');
	item.classList.add(`bg-${color}`);
	item.style.background = color;
	item.textContent = color;
	fragment.appendChild(item);
});

document.appendChild(fragment);
```

Добавятся три дива с классами `bg-black`, `bg-yellow`, `bg-orange` и текстовым содержимым `black`, `yellow`,`orange` для каждого из дивов соответственно.

