```css
body {
  counter-reset: section; /* Устанавливает значение
                                                 счётчика, равным 0 */
}

h3::before {
  counter-increment: section; /* Инкрементирует счётчик*/
  content: "Секция " counter(section) ": "; /* Отображает текущее значение счётчика */
}
```

```html
<h3>Вступление</h3>
<h3>Основная часть</h3>
<h3>Заключение</h3>
```

![[Pasted image 20240329013908.png]]

Позволяет использовать счетчики в CSS
- counter-reset - инициализирует и задает имя счетчику
- counter-increment - увеличивает счетчик
- counter-set - устанавливает значение счетчику. Это не инициализация, установить значение можно только после объявления счетчика через `counter-reset`

Примеры:
```css
/* Create a counter with initial default value 0 */
counter-reset: my-counter;

/* Create a counter and initialize as "-3" */
counter-reset: my-counter -3;

/* Create a reversed counter with initial default value */
counter-reset: reversed(my-counter);

/* Create a reversed counter and initialize as "-1" */
counter-reset: reversed(my-counter) -1;

/* Create reversed and regular counters at the same time */
counter-reset: reversed(pages) 10 items 1 reversed(sections) 4;

/* Remove all counter-reset declarations in less specific rules */
counter-reset: none;

/* Global values */
counter-reset: inherit;
counter-reset: initial;
counter-reset: revert;
counter-reset: revert-layer;
counter-reset: unset;
```

```css
h1 {
  /* Create the counters "chapter" and "page" and set to initial default value.
     Create the counter "section" and set to "4". */
  counter-reset: chapter section 4 page;
}
```