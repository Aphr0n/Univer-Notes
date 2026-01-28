Singleton — це шаблон проектування, який обмежує створення екземплярів класу одним об'єктом. Це корисно, коли для координації дій по всій системі потрібен лише один об'єкт.
```Java
public class MyClass {
	private static final MyClass uniqueInstance = new MyClass();
...
	private MyClass() { ... }
	public static MyClass getInstance() {
	return uniqueInstance;
	}
...
}
```