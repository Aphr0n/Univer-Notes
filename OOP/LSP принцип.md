Функції, що використовують посилання на базові (супер) класи, повинні мати можливість використовувати об'єкти похідних (під) класів, не знаючи цього

```Java
public class Rectangle {
	private double width;
	private double height;
	public Rectangle(double width, double height) {
		this.width = width;
		this.height = height;
	}
	public double getWidth() { return this.width; }
	public void setWidth(double width) { this.width = width; }
	public double getHeight() { return this.height; }
	public void setHeight(double height) { this.height = height; }
	public double area() { return this.width * this.height; }
}
```
- Тут ми намагаємося зробити`Square` підкласом`Rectangle`.
- Проблема: якщо код очікує, що `Rectangle` можна змінювати ширину і висоту окремо, а `Square` змінює обидві сторони одночасно, **LSP порушується**.