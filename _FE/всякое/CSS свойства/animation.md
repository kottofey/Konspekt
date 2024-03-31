Сокращенная запись выглядит следующим образом:

`animation: animation-duration || animation-timing-function> || animation-delay || animation-iteration-count || animation-direction || animation-fill-mode || animation-play-state || [ none | <keyframes-name> ]`

Например:
```css
p {
  animation-duration: 3s;
  animation-name: slidein;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}

можно заменить на

p {
  animation: 3s infinite alternate slidein;
}
```

