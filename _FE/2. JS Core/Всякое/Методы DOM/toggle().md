Переключает классы
```js
элемент.classList.toggle('класс');
элемент.classList.toggle('класс', force);
```

Если класса не было, то метод добавляет его и возвращает `true`. Если класс уже был, значит метод его уберёт и возвратит `false`.

Опция `force` делает этот метод односторонним. То есть, выполняется только первое действие. Если класс был, то он только уберётся и метод вернёт `false`, а если класса не было, то он только установится и метод вернёт `true`. И всё. 