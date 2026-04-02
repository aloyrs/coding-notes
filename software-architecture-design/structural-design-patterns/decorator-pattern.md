# 🎁 Decorator Pattern – Overview

### 🧠 Concept

The **Decorator Pattern** lets you **add new behavior to objects dynamically**
without changing their original code or using inheritance.

> 💡 Think of it as _“wrapping” an object_ with extra features — like adding gift wrap or toppings on a pizza.

---

### 🧱 Key Roles

| Role                  | Description                                                              |
| --------------------- | ------------------------------------------------------------------------ |
| **Component**         | The base interface or abstract class (defines the main behavior).        |
| **ConcreteComponent** | The original object to be decorated.                                     |
| **Decorator**         | Wraps a component and implements the same interface.                     |
| **ConcreteDecorator** | Adds extra behavior before or after delegating to the wrapped component. |
| **Client**            | Works with components and decorators interchangeably.                    |

---

### 💻 Java Example – UI Example (TextField with Scrollbars & Borders)

```java
// ----- Component -----
interface UIComponent {
    void render();
}

// ----- Concrete Component -----
class TextField implements UIComponent {
    public void render() {
        System.out.println("Rendering basic text field");
    }
}

// ----- Base Decorator -----
abstract class UIComponentDecorator implements UIComponent {
    protected UIComponent component;

    public UIComponentDecorator(UIComponent component) {
        this.component = component;
    }

    public void render() {
        component.render(); // delegate to wrapped component
    }
}

// ----- Concrete Decorators -----
class BorderDecorator extends UIComponentDecorator {
    public BorderDecorator(UIComponent component) {
        super(component);
    }

    public void render() {
        super.render();
        System.out.println("→ Adding border decoration");
    }
}

class ScrollbarDecorator extends UIComponentDecorator {
    public ScrollbarDecorator(UIComponent component) {
        super(component);
    }

    public void render() {
        super.render();
        System.out.println("→ Adding scrollbar decoration");
    }
}

// ----- Client -----
public class Main {
    public static void main(String[] args) {
        // Start with a plain text field
        UIComponent textField = new TextField();

        // Decorate it with scrollbar
        UIComponent scrollable = new ScrollbarDecorator(textField);

        // Further decorate with border
        UIComponent borderedScrollable = new BorderDecorator(scrollable);

        borderedScrollable.render();
    }
}
```

**Output:**

```
Rendering basic text field
→ Adding scrollbar decoration
→ Adding border decoration
```

---

### 🧠 Flow Summary

| Step | Action                         | Result                          |
| ---- | ------------------------------ | ------------------------------- |
| 1️⃣   | Start with `TextField`         | Basic component                 |
| 2️⃣   | Wrap with `ScrollbarDecorator` | Adds scrolling                  |
| 3️⃣   | Wrap with `BorderDecorator`    | Adds border                     |
| ✅   | Final render                   | Combines all layers dynamically |

> 🧩 You can add or remove decorators at runtime — flexible layering of behavior.

---

### 🪜 Summary

- Adds functionality **without modifying existing classes**.
- Promotes **composition over inheritance**.
- Each decorator is **interchangeable** with the original component.
- Commonly used for **UI elements, streams, and logging** in Java.

---

### 🧾 Real-world Analogy

☕ **Coffee Order System**

- Base = Plain coffee
- Decorators = Milk, Sugar, Caramel, Whipped Cream
- You “wrap” the coffee with each topping → new flavor each time.

💡 The coffee object doesn’t change — decorators just add layers.

---

### 🧭 TL;DR

> **Decorator Pattern = Add behavior dynamically by wrapping objects.**
> “Flexible alternative to subclassing for extending functionality.”
