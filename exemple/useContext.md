## Как работает useContext()?

1. Создаем контекст (коробку для данных).
2. Кладем данные в контекст с помощью *Provider.*
3. Достаем данные из контекста с помощью *useContext()*

---
Пример: Передача темы (светлая/темная)
### 1. Создаем контекст
   Создаем "коробку" для данных с помощью **createContext()**.
```jsx
import React from 'react';

const ThemeContext = React.createContext(); // Создали коробку
```
### 2. Кладем данные в контекст с помощью *Provider* 

```jsx
function App() {
  const [theme, setTheme] = React.useState('light'); // Состояние темы

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Header />
      <Button />
    </ThemeContext.Provider>
  );
}
```
*Здесь:*

- *ThemeContext.Provider* — это коробка, в которую мы положили данные.

- *value={{ theme, setTheme }}* — это данные, которые мы передаем (текущая тема и функция для её изменения).

### 3. Достаем данные из контекста

Теперь в любом компоненте (например, Button) мы можем достать данные из коробки с помощью *useContext()*.

```jsx
import React, { useContext } from 'react';

function Button() {
  const { theme, setTheme } = useContext(ThemeContext); // Достаем данные из коробки

  const toggleTheme = () => {
    setTheme(theme === 'light' ? 'dark' : 'light'); // Меняем тему
  };

  return (
    <button
      onClick={toggleTheme}
      style={{
        backgroundColor: theme === 'light' ? '#fff' : '#333',
        color: theme === 'light' ? '#000' : '#fff',
      }}
    >
      Сменить тему
    </button>
  );
}
```
---
**Что происходит в этом примере?**
1. В App мы создаем состояние темы (theme) и кладем его в коробку (ThemeContext.Provider).

2. В компоненте Button мы достаем тему и функцию для её изменения из коробки с помощью useContext().

3. Когда пользователь нажимает на кнопку, тема меняется.

---
### Итог:
- **useContext()** — это способ легко доставать данные из контекста.

- Не нужно передавать данные через пропсы на каждом уровне.

- Используй **useContext()**, когда у тебя есть данные, которые нужны многим компонентам (например, тема, настройки, данные пользователя).

