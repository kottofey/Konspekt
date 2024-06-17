Аттрибуты, начинающиеся с data-* называются data-аттрибутами и содержат дополнительную информацию, к которой можно получить доступ из CSS и JS. 

В CSS доступ получается при помощи функции attr(). Пример:

```html
<article
  id="electriccars"
  data-columns="3"
  data-index-number="12314"
  data-parent="cars">
  ...
</article>

```

```css
article::before {
  content: attr(data-parent);
}
```

