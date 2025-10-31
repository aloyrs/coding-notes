# 🧬 Prototype Pattern – Overview

### 🧠 Concept

The **Prototype Pattern** creates new objects by **cloning existing ones** (prototypes),
instead of creating them from scratch.

> 💡 Think of it as *“copy–paste” object creation* — efficient when initialization is expensive or complex.

---

### 🧱 Key Roles

| Role                  | Description                                                        |
| --------------------- | ------------------------------------------------------------------ |
| **Prototype**         | Declares a cloning interface (e.g., `clone()` method).             |
| **ConcretePrototype** | Implements the cloning method.                                     |
| **Client**            | Uses the prototype to create new objects by copying existing ones. |

---

### 💻 Java Example – UI Button Prototype

```java
// ----- Prototype Interface -----
interface UIComponent extends Cloneable {
    UIComponent clone();
    void render();
}

// ----- Concrete Prototype -----
class Button implements UIComponent {
    private String color;
    private String label;

    public Button(String color, String label) {
        this.color = color;
        this.label = label;
    }

    // Clone method
    public UIComponent clone() {
        return new Button(this.color, this.label);
    }

    public void render() {
        System.out.println("Button: " + label + " [" + color + "]");
    }
}

// ----- Another Concrete Prototype -----
class Checkbox implements UIComponent {
    private boolean checked;

    public Checkbox(boolean checked) {
        this.checked = checked;
    }

    public UIComponent clone() {
        return new Checkbox(this.checked);
    }

    public void render() {
        System.out.println("Checkbox: " + (checked ? "Checked" : "Unchecked"));
    }
}

// ----- Client -----
class PrototypeRegistry {
    private Map<String, UIComponent> prototypes = new HashMap<>();

    public void register(String key, UIComponent prototype) {
        prototypes.put(key, prototype);
    }

    public UIComponent create(String key) {
        UIComponent prototype = prototypes.get(key);
        return prototype != null ? prototype.clone() : null;
    }
}
```

✅ **Usage Example:**

```java
public class Main {
    public static void main(String[] args) {
        PrototypeRegistry registry = new PrototypeRegistry();

        // Register prototypes
        registry.register("blueButton", new Button("blue", "Submit"));
        registry.register("checkedBox", new Checkbox(true));

        // Clone new components
        UIComponent btn1 = registry.create("blueButton");
        UIComponent box1 = registry.create("checkedBox");

        btn1.render();
        box1.render();
    }
}
```

**Output:**

```
Button: Submit [blue]
Checkbox: Checked
```

---

### 🧠 Flow Summary

| Step | Action                                 | Result                                     |
| ---- | -------------------------------------- | ------------------------------------------ |
| 1️⃣  | Register prototype objects in registry | “Blueprints” stored                        |
| 2️⃣  | Client requests a new component        | Registry clones the prototype              |
| 3️⃣  | Client gets a **fresh copy**           | Fast creation, same structure as prototype |

---

### 🪜 Summary

* Used when creating objects is **expensive or repetitive**.
* Allows **cloning existing instances** instead of building new ones.
* Makes adding new types easier — just register new prototypes.
* Avoids subclass explosion (no need for many factory subclasses).

---

### 🧾 Real-world Analogy

🖨️ **Document Template System**

* You duplicate a “Letter Template” or “Invoice Template”
  instead of writing from scratch.
* The new copy (clone) can then be modified independently.

---

### 🧭 TL;DR

> **Prototype Pattern = Clone existing objects to create new ones.**
> Efficient, flexible, and reduces dependency on constructors.