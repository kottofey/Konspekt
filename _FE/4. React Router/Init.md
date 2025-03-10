- Устанавливаем Роутер
```sh
npm install react-router-dom
```

- Импортируем и создаём роутер. В массиве-аргументе прописываем объекты-роуты
```jsx
import {
  createBrowserRouter,
  RouterProvider,
} from "react-router-dom";


const router = createBrowserRouter([
  {
    path: "/",
    element: <div>Hello world!</div>,
  },
  {
    path: "/contacts/:contactId",
    element: <Contact />,
  }
]);
```

# Вложенные роуты
Чтобы сделать так, что элемент рендерился внутри роута, который уже на экране, нужно сделать этот элемент дочерним и указать ГДЕ ему нужно отрендериться. Это можно сделать с помощью компонента `<Outlet />`, его нужно прописать внутри jsx где ему нужно отбразиться:
```jsx title=main.jsx
import {
  createBrowserRouter,
  RouterProvider,
} from "react-router-dom";


const router = createBrowserRouter([
  {
    path: "/",
    element: <div>Hello world!</div>,
    children: [
      {
        path: "/contacts/:contactId",
        element: <Contact />,
      }
  ]
  },
]);
```

```jsx title=root.jsx
import { Outlet } from "react-router-dom";

export default function Root() {
  return (
    <>
      {/* all the other elements */}
      <div id="detail">
        <Outlet />
      </div>
    </>
  );
}
```

С помощью `<Outlet />` мы говорим где нужно рендерить дочерние компоненты

# Роутинг на стороне клиента
Если оставить ссылки, как есть, то при клике будет послан запрос на сервер и страница полностью перезагрузится. Чтобы этого не происходило, ссылки оборачиваются в компонент `<Link />`. Это кеширует запросы и новых не происходит, если страница была уже посещена.

```jsx title=root.jsx
import { Outlet, Link } from "react-router-dom";

export default function Root() {
  return (
    <>
      <div id="sidebar">
        {/* other elements */}

        <nav>
          <ul>
            <li>
              <Link to={`contacts/1`}>Your Name</Link>
            </li>
            <li>
              <Link to={`contacts/2`}>Your Friend</Link>
            </li>
          </ul>
        </nav>

        {/* other elements */}
      </div>
    </>
  );
}
```

