```jsx
import React, { useRef } from 'react';

function InputFocus() {
  // Создаем ссылку на DOM-элемент
  const inputRef = useRef(null);

  // Функция для фокусировки на input
  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="Введите текст" />
      <button onClick={focusInput}>Фокусировать input</button>
    </div>
  );
}

export default InputFocus;
```
Создание ссылки:

```jsx
const inputRef = useRef(null);
```
*useRef* создает объект { current: null }, где current будет хранить ссылку на DOM-элемент.

Привязка ссылки к элементу:
```jsx
<input ref={inputRef} type="text" placeholder="Введите текст" />
```
Атрибут ref связывает inputRef с элементом input.

Использование ссылки:
```jsx
inputRef.current.focus();
```
*inputRef.current* содержит ссылку на DOM-элемент, и мы можем вызывать его методы, например, focus().
___
***ТАКЖЕ useRef используется для хранения предыдущего значения например таймера***
```jsx
const [count, setCount] = useState(0);
const prevCountRef = useRef();

// Сохраняем текущее значение count в ref перед обновлением
useEffect(() => {
    prevCountRef.current = count;
}, [count]);
```
Получение значения рефа:

```jsx
console.log(myRef.current); // Получение значения рефа
```

___
***Когда использовать useRef:***
Доступ к DOM-элементам: Например, фокусировка на input, управление видео или анимациями.

Хранение изменяемых значений: Например, таймеры, интервалы или предыдущие значения.

Избежание ререндеров: Если изменение значения не должно вызывать ререндер компонента.

***Важные моменты:***
useRef возвращает объект { current: initialValue }, где current — это изменяемое значение.

Изменение current *не вызывает ререндер компонента.*

useRef можно использовать для любых изменяемых значений, а не только для DOM-элементов.