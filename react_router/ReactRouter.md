1. Настройка маршрутизации

Основные компоненты React Router v6:

    BrowserRouter (или HashRouter) — обертка для всего приложения.
    Routes — контейнер для определения маршрутов.
    Route — отдельный маршрут, связывающий URL с компонентом.
    Link — компонент для навигации между страницами.
    Navigate — для программной навигации или перенаправления.
    Outlet — используется для вложенных маршрутов.
    useNavigate, useParams, useLocation — хуки для работы с маршрутизацией.

<details> 
<summary> Пример базовой настройки</summary>

```jsx
import React from 'react';
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <ul>
          <li><Link to="/">Главная</Link></li>
          <li><Link to="/about">О нас</Link></li>
          <li><Link to="/contact">Контакты</Link></li>
        </ul>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </BrowserRouter>
  );
}

function Home() {
  return <h1>Добро пожаловать на главную страницу!</h1>;
}

function About() {
  return <h1>Страница "О нас"</h1>;
}

function Contact() {
  return <h1>Страница контактов</h1>;
}

export default App;
```
</details>

2. Вложенные маршруты

React Router v6 поддерживает вложенные маршруты через компонент **Outlet**. Это полезно для создания макетов с общими элементами (например, шапкой или боковой панелью). 

<details>
<summary> Пример вложенных маршрутов</summary>

```jsx
import React from 'react';
import { BrowserRouter, Routes, Route, Link, Outlet } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Layout />}>
          <Route index element={<Home />} />
          <Route path="about" element={<About />} />
          <Route path="contact" element={<Contact />} />
        </Route>
      </Routes>
    </BrowserRouter>
  );
}

function Layout() {
  return (
    <div>
      <nav>
        <ul>
          <li><Link to="/">Главная</Link></li>
          <li><Link to="about">О нас</Link></li>
          <li><Link to="contact">Контакты</Link></li>
        </ul>
      </nav>

      <hr />
      <Outlet /> {/* Здесь будут отображаться дочерние маршруты */}
    </div>
  );
}

function Home() {
  return <h1>Главная страница</h1>;
}

function About() {
  return <h1>Страница "О нас"</h1>;
}

function Contact() {
  return <h1>Страница контактов</h1>;
}

export default App;
```
</details>

3. Динамические маршруты

Для создания динамических маршрутов используйте параметры **(:paramName)** в пути. 

<details>
<summary> Пример динамических маршрутов</summary>

**useParams** — это хук, который предоставляется библиотекой React Router и позволяет получить параметры текущего маршрута.

```jsx
import React from 'react';
import { BrowserRouter, Routes, Route, Link, useParams } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <ul>
          <li><Link to="/users/1">Пользователь 1</Link></li>
          <li><Link to="/users/2">Пользователь 2</Link></li>
        </ul>
      </nav>

      <Routes>
        <Route path="/users/:id" element={<User />} />
      </Routes>
    </BrowserRouter>
  );
}

function User() {
  const { id } = useParams(); // Получаем параметр из URL
  return <h1>Пользователь с ID: {id}</h1>;
}

export default App;
```
</details>

4. Перенаправление

**Navigate** используется для программной навигации, позволяя вам перенаправлять пользователей на другие маршруты. Это полезно, когда нужно выполнить перенаправление на основе логики вашего приложения, такой как авторизация или условия выполнения

<details>
<summary> Пример перенаправления</summary>

```jsx
import React from 'react';
import { BrowserRouter, Routes, Route, Navigate } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/old-page" element={<Navigate to="/" />} />
      </Routes>
    </BrowserRouter>
  );
}

function Home() {
  return <h1>Главная страница</h1>;
}

export default App;
```
</details>

<details>
<summary> Пример перенаправления при логировании</summary>

```jsx
import React from 'react';
import { Navigate } from 'react-router-dom';

const ProtectedRoute = ({ isAuthenticated, children }) => {
  if (!isAuthenticated) {
    // Если пользователь не авторизован, перенаправляем на страницу входа
    return <Navigate to="/login" replace />;
  }

  return children;
};

export default ProtectedRoute;
```
компонент *ProtectedRoute* принимает проп *isAuthenticated* для проверки авторизации пользователя. Если пользователь не авторизован, **Navigate** перенаправит его на страницу входа (/login). Используя проп *replace*, мы заменяем текущий маршрут новым, что предотвращает добавление перенаправления в историю браузера.
</details>


5. Программная навигация

Для программной навигации используйте хук useNavigate
<details>
<summary> Пример программной навигации</summary>

**useNavigate** из React Router используется для программной навигации внутри вашего приложения. Он возвращает функцию, которую можно использовать для навигации к разным маршрутам.

navigate для выполнения более сложных действий, таких как передача состояний и замена текущего маршрута. Вот несколько примеров
1. Передача состояния:
```jsx
navigate('/about', { state: { fromHome: true } });
```
2. Замена текущего маршрута (не добавляет новый маршрут в историю браузера):
```jsx
navigate('/about', { replace: true });
```
3.Перенаправление назад:
```jsx
navigate(-1); // Возвращает на один шаг назад в истории
```

```jsx
import React from 'react';
import { BrowserRouter, Routes, Route, useNavigate } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/dashboard" element={<Dashboard />} />
      </Routes>
    </BrowserRouter>
  );
}

function Home() {
  const navigate = useNavigate();

  const goToDashboard = () => {
    navigate('/dashboard');
  };

  return (
    <div>
      <h1>Главная страница</h1>
      <button onClick={goToDashboard}>Перейти на Dashboard</button>
    </div>
  );
}

function Dashboard() {
  return <h1>Dashboard</h1>;
}

export default App;
```
</details>

5. Обработка ошибок (NotFound)

<details>
<summary> Пример Обработки ошибок</summary>
Чтобы отобразить страницу ошибки для несуществующих маршрутов, используйте <b>path="*"</b>>

```jsx
import React from 'react';
import { BrowserRouter, Routes, Route } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}

function Home() {
  return <h1>Главная страница</h1>;
}

function NotFound() {
  return <h1>Страница не найдена</h1>;
}

export default App;
```
</details>

6. Активные ссылки

<details>
<summary> Пример Активных ссылок</summary>

Для выделения активных ссылок используйте компонент **NavLink**

```jsx  
import React from 'react';
import { BrowserRouter, Routes, Route, NavLink } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <ul>
          <li>
            <NavLink
              to="/"
              style={({ isActive }) => ({ color: isActive ? 'red' : 'black' })}
            >
              Главная
            </NavLink>
          </li>
          <li>
            <NavLink
              to="/about"
              style={({ isActive }) => ({ color: isActive ? 'red' : 'black' })}
            >
              О нас
            </NavLink>
          </li>
        </ul>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}

function Home() {
  return <h1>Главная страница</h1>;
}

function About() {
  return <h1>Страница "О нас"</h1>;
}

export default App;
```
</details>

7. React Router предоставляет несколько полезных хуков:


    useParams — для получения параметров маршрута.
    useNavigate — для программной навигации.
    useLocation — для получения текущего местоположения.
    useMatch — для проверки совпадения маршрута.
     
