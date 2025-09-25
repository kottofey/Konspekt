Для пути можно указать несколько middleware: 

```ts
// Обработчик маршрута
const handler: RequestHandler = async (req, res, next) => {
  try {
    // Ваша логика
    res.send("Успешный ответ");
  } catch (error) {
    next(error);
  }
};

// Маршрут
app.get(
  `/api/v1/${routeName}`,
  middleware1,
  middleware2,      
  handler
);
```

Самое главное в миддлварях чтобы они либо вызывали next(), либо явно заканчивали вызов через return при любом из раскладов. Иначе будет ошибка.