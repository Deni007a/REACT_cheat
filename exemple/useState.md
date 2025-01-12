```jsx
import React, { useState } from 'react';

function Counter() {
// Используем useState для создания состояния
const [count, setCount] = useState(0);

// Функция для увеличения счетчика
const increment = () => {
setCount(count + 1);
};

// Функция для сброса счетчика
const reset = () => {
setCount(0);
};

return (
<div>
<h1>Счетчик: {count}</h1>
<button onClick={increment}>Увеличить</button>
<button onClick={reset}>Сбросить</button>
</div>
);
}

export default Counter;
```
*Импорт useState*:
```jsx
import React, { useState } from 'react';
```
*Инициализация состояния:*

```jsx
const [count, setCount] = useState(0);
```
useState(0) инициализирует состояние с начальным значением 0.

**count** — это текущее значение состояния.

**setCount** — это функция, которая позволяет обновлять значение count.

*Обновление состояния:*

```jsx
const increment = () => {
setCount(count + 1);
};
```
Когда вызывается setCount(count + 1), значение count увеличивается на 1, и компонент перерисовывается с новым значением.

*Сброс состояния:*
```jsx
const reset = () => {
setCount(0);
};
```
Функция reset сбрасывает значение count обратно к 0.

Отображение состояния:
```jsx
<h1>Счетчик: {count}</h1>
```
Текущее значение count отображается в заголовке.

Кнопки для управления состоянием:

```jsx
<button onClick={increment}>Увеличить</button>
<button onClick={reset}>Сбросить</button>
```


Как это работает:
При нажатии на кнопку "Увеличить" вызывается функция increment, которая увеличивает значение count на 1.

При нажатии на кнопку "Сбросить" вызывается функция reset, которая сбрасывает значение count к 0.

Каждый раз, когда состояние изменяется, компонент перерисовывается, и новое значение count отображается на экране.