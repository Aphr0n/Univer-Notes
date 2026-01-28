`this` - це посилання на поточний об'єкт (об'єкт, метод або конструктор якого викликається). Можна звернутися до будь-якого члена поточного об'єкта зсередини методу екземпляра або конструктора, використовуючи це
Об'єктно-орієнтовані мови програмування реалізують посилання на поточний об'єкт
- Для доступу до затінених членів класу
- Для посилання на себе

# Використання this зі змінними екземпляра
Найпоширеніша причина використання ключового слова this полягає в тому, що змінна екземпляра затінена параметром методу або конструктора. Кожен аргумент конструктора затінює одну зі змінних екземпляра – всередині конструктора price знаходиться локальна копія першого аргументу конструктора. Щоб звернутися до члена Article price, конструктор повинен використовувати this.price
```Java
public class Article {
	private String name;
	private int quantity;
	private double price;
	public Article(String newName, int newQuantity, double newPrice) {
		name = newName;
		quantity = newQuantity;
		price = newPrice;
}
...
}
```
Кращий варіант цієї ж програми:
```Java
public class Article {
	private String name;
	private int quantity;
	private double price;
	public Article(String name, int quantity, double price) {
		this.name = name;
		this.quantity = quantity;
		this.price = price;
}
...
}
```
# Використання this з конструктором
Явний виклик конструктора - це виклик іншого конструктору класy через this. Іншими словами це спосіб вибрати конструктор за замовчуванням, через який **пройде уся ініціалізація** 

```Java
public class Article {
	private String name;
	private int quantity;
	private double price;
	public Article() {
	this("", 0, 0.0);
}
public Article(String name, int quantity, double price) {
	this.name = name;
	this.quantity = quantity;
	this.price = price;
}
...
}
```

- Для цього класу є два конструктори для ініціалізації змінних екземпляра
- Конструктор без аргументів надає значення за замовчуванням для всіх змінних екземпляра
- Оскільки початкові значення не надаються аргументами
- Конструктор без аргументів викликає конструктор з трьома аргументами з трьома значеннями за замовчуванням
- Якщо присутній, виклик іншого конструктора має бути першим рядком у конструкторі