```jsx
useEffect(() => {
    // Логика побочного эффекта

    return () => {
        // Логика очистки (опционально)
    };
}, [зависимости]);
```

**Первый аргумент**: Функция, содержащая логику побочного эффекта.

**Второй аргумент** (опционально): Массив зависимостей. Эффект будет выполняться только если одна из зависимостей
изменилась
с момента последнего рендера. Если массив пустой [], эффект *выполнится только один раз* после первого рендера. Если
аргумент опущен, эффект будет *выполняться после каждого рендера*.

---

### Основные случаи использования

Выполнить эффект один раз (при монтировании):

```jsx
useEffect(() => {
    console.log("Компонент смонтирован");
    return () => {
        console.log("Компонент размонтирован");
    };
}, []);
```

Выполнить эффект при изменении определённого состояния или пропса:

```jsx
const [count, setCount] = useState(0);

useEffect(() => {
    console.log(`Значение count изменилось на ${count}`);
}, [count]); // Эффект выполнится только при изменении `count`
```

Очистка побочных эффектов (например, таймеры или подписки):

```jsx
useEffect(() => {
    const timer = setInterval(() => {
        console.log("Тик таймера");
    }, 1000);

    return () => {
        clearInterval(timer); // Очистка таймера при размонтировании
    };
}, []);
```

Запрос данных:

```jsx
const [data, setData] = useState(null);

useEffect(() => {
    fetch("https://api.example.com/data")
        .then((response) => response.json())
        .then((data) => setData(data))
        .catch((error) => console.error("Ошибка при запросе данных:", error));
}, []); // Выполнится только один раз при монтировании
```

### Важные моменты

- **Массив зависимостей:** Всегда указывайте зависимости, от которых зависит ваш эффект. Если этого не сделать, могут
  возникнуть баги или лишние ререндеры.
- **Очистка:** Используйте функцию очистки, чтобы избежать утечек памяти или нежелательного поведения (например, очистка
  таймеров или отписка от событий).
- **Бесконечные циклы:** Убедитесь, что эффект не обновляет состояние или пропсы, которые могут вызвать его повторное
  выполнение, приводящее к бесконечному циклу.

Пример: Использование useEffect с состоянием

```jsx
import React, {useState, useEffect} from "react";

function Counter() {
    const [count, setCount] = useState(0);

    useEffect(() => {
        document.title = `Счётчик: ${count}`;
    }, [count]); // Обновляет заголовок документа при изменении `count`

    return (
        <div>
            <p>Счётчик: {count}</p>
            <button onClick={() => setCount(count + 1)}>Увеличить</button>
        </div>
    );
}

export default Counter;
```

тут useEffect обновляет заголовок документа каждый раз, когда изменяется состояние count.

Эффект выполняется только при изменении count, так как он указан в массиве зависимостей.
