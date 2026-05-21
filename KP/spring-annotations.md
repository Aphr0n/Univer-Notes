# Spring MVC — Анотації

## Анотації класу

### `@Controller`
Позначає клас як Spring MVC контролер. Spring знаходить його при скануванні і реєструє.
Методи повертають **назву шаблону** (наприклад `"index"`), а не JSON.
> Відрізняється від `@RestController` — той повертає JSON напряму.

### `@RequestMapping("/path")`
Базовий шлях для всіх методів класу.
```java
@RequestMapping("/unpuzzle")
// всі методи всередині будуть відносно /unpuzzle
```

### `@SessionAttributes("name")`
Зберігає вказаний атрибут моделі в HTTP-сесії між запитами.
Об'єкт живе поки жива сесія (закрив вкладку / таймаут → зникає).
```java
@SessionAttributes("unpuzzleState")
// стан гри зберігається між кліками
```

---

## Анотації методів

### `@GetMapping` / `@PostMapping("/path")`
Прив'язує метод до HTTP GET або POST запиту.
```java
@GetMapping                  // GET /unpuzzle
@PostMapping("/move")        // POST /unpuzzle/move
```

### `@ModelAttribute("name")` на методі
Метод викликається **автоматично перед кожним запитом**.
Завдяки `@SessionAttributes` — тільки якщо об'єкта ще немає в сесії (тобто перший візит).
```java
@ModelAttribute("unpuzzleState")
public UnpuzzleWebState initState() {
    return new UnpuzzleWebState(9, 9); // ініціалізація при першому відвідуванні
}
```

---

## Анотації параметрів

### `@ModelAttribute("name")` на параметрі
Дістає об'єкт з сесії/моделі і підставляє в параметр автоматично.
Без цього довелося б писати вручну:
```java
// без Spring:
UnpuzzleWebState state = (UnpuzzleWebState) httpSession.getAttribute("unpuzzleState");

// зі Spring:
public String show(@ModelAttribute("unpuzzleState") UnpuzzleWebState state, ...) { ... }
```

### `@RequestParam("name")`
Бере параметр з HTTP-запиту (з форми або query string) і підставляє в параметр методу.
Автоматично конвертує тип (String → int тощо).
```java
@RequestParam("tileRow") int tileRow   // бере ?tileRow=3 і конвертує в int
```

---

## Параметри без анотацій (Spring підставляє сам)

| Тип | Що підставляє |
|---|---|
| `Model` | Об'єкт для передачі даних у шаблон (`model.addAttribute(...)`) |
| `Authentication` | Поточний користувач зі Spring Security (або `null` / anonymous) |
| `HttpSession` | HTTP-сесія напряму (якщо потрібна) |

---

## Загальна схема роботи

```
Браузер (форма/кнопка)
        ↓  POST/GET запит
Контролер — обробляє логіку, заповнює Model
        ↓
Thymeleaf — підставляє дані з Model через th:*
        ↓
Готовий HTML → браузер
```

> **Post/Redirect/Get патерн:** після POST контролер робить `redirect:/unpuzzle`,
> що викликає GET, який вже рендерить шаблон.
> Це запобігає повторному відправленню форми при натисканні F5.

---

## Рівні "пам'яті" в Spring

| | Живе | Аналогія |
|---|---|---|
| `Model` | 1 запит | локальна змінна |
| `@SessionAttributes` | поки жива сесія | поточний контекст |
| `@ApplicationScope` / static | поки живе додаток | глобальна змінна |
