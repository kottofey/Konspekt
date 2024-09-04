Позволяет получить _полную_ информацию о свойстве.

Его синтаксис:

```javascript
let descriptor = Object.getOwnPropertyDescriptor(obj, propertyName);
```

`obj`

Объект, из которого мы получаем информацию.

`propertyName`

Имя свойства.

Возвращаемое значение – это объект, так называемый «дескриптор свойства»: он содержит значение свойства и все его флаги.

Например:

```javascript
let user = {
  name: "John"
};

let descriptor = Object.getOwnPropertyDescriptor(user, 'name');

alert( JSON.stringify(descriptor, null, 2 ) );
/* дескриптор свойства:
{
  "value": "John",
  "writable": true,
  "enumerable": true,
  "configurable": true
}
*/
```