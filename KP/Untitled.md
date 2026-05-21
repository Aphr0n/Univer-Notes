● JPA (Java Persistence API) — це стандарт, який дозволяє працювати з базою даних через Java-об’єкти, а не писати SQL всюди. Це називається ORM (об’єкт ↔ рядок у таблиці).

  У цьому проєкті:

   - @Entity (наприклад Score.java) каже: “цей клас — таблиця”.
   - @Id @GeneratedValue каже: “це первинний ключ, генерується автоматично”.
   - EntityManager у ScoreServiceJPA.java — головний інструмент JPA:
   - persist(score) → вставити в БД
   - createQuery/NamedQuery → вибрати з БД (JPQL, схоже на SQL, але про сутності)
   - @Transactional → усі операції виконуються як одна транзакція.
   - Реально виконує JPA тут Hibernate (залежності в pom.xml).


● REST — це спосіб зробити “веб-доступ” до твоєї програми через HTTP (як у браузері), де кожен ресурс має URL, а дії робляться HTTP-методами.

  У цьому проєкті REST зроблений через Spring:

  1) REST-контролер = “вхідні двері”

  Напр. ScoreServiceRest.java:

   - @RestController — каже Spring: “це API, відповідь буде даними (JSON), не HTML”
   - @RequestMapping("/api/score") — базовий шлях

  2) Маршрути (endpoints) і методи

   - GET /api/score/{game} (@GetMapping("/{game}"))
   - повертає List<Score> → Spring автоматично серіалізує в JSON
   - POST /api/score (@PostMapping)
   - приймає JSON в @RequestBody Score score → Spring автоматично перетворює JSON у Java-об’єкт
   - DELETE /api/score/reset (@DeleteMapping("/reset"))
   - очищає дані


● Spring — це “каркас”, який збирає твою програму як конструктор: сам створює об’єкти, з’єднує їх і запускає веб‑сервер.

  На прикладі цього проєкту:

   - GameStudioServer.java з @SpringBootApplication — старт: SpringApplication.run(...) піднімає сервер (Tomcat) і весь застосунок.
   - DI/IoC (впорскування залежностей): методи @Bean створюють сервіси (ScoreServiceJPA, RatingServiceJPA…), а в REST-контролерах @Autowired підставляє їх автоматично.
   - @RestController — робить HTTP API.
   - @EntityScan("...entity") + spring-boot-starter-data-jpa — підключає JPA/Hibernate.
   - application.properties — налаштування БД і JPA.
