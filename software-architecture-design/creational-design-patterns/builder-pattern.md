# 🧱 Builder Pattern – Overview

### 🧠 Concept

The **Builder Pattern** lets you **construct complex objects step by step**.
It separates the **construction process** from the **final representation**,
so the same process can create different representations.

> 💡 Think of it as assembling a burger, a car, or a dialog box — piece by piece.

---

### 🧱 Key Roles

| Role                | Description                                           |
| ------------------- | ----------------------------------------------------- |
| **Builder**         | Declares the steps to build the product.              |
| **ConcreteBuilder** | Implements the building steps for a specific product. |
| **Product**         | The final object being built.                         |
| **Director**        | Controls the construction order.                      |
| **Client**          | Tells the Director what type of product to build.     |

---

### 💻 Java Example – UI Dialog Builder

```java
// ----- Product -----
class Dialog {
    private String title;
    private String message;
    private String okButton;
    private String cancelButton;

    public void setTitle(String title) { this.title = title; }
    public void setMessage(String message) { this.message = message; }
    public void setOkButton(String okButton) { this.okButton = okButton; }
    public void setCancelButton(String cancelButton) { this.cancelButton = cancelButton; }

    public void show() {
        System.out.println("Dialog: " + title);
        System.out.println("Message: " + message);
        System.out.println("[ " + okButton + " ] [ " + cancelButton + " ]");
    }
}

// ----- Builder Interface -----
interface DialogBuilder {
    void buildTitle(String title);
    void buildMessage(String message);
    void buildOkButton(String text);
    void buildCancelButton(String text);
    Dialog getDialog();
}

// ----- Concrete Builder -----
class AlertDialogBuilder implements DialogBuilder {
    private Dialog dialog = new Dialog();

    public void buildTitle(String title) { dialog.setTitle(title); }
    public void buildMessage(String message) { dialog.setMessage(message); }
    public void buildOkButton(String text) { dialog.setOkButton(text); }
    public void buildCancelButton(String text) { dialog.setCancelButton(text); }
    public Dialog getDialog() { return dialog; }
}

// ----- Director -----
class DialogDirector {
    private DialogBuilder builder;

    public DialogDirector(DialogBuilder builder) { this.builder = builder; }

    public Dialog constructWarningDialog() {
        builder.buildTitle("Warning");
        builder.buildMessage("Unsaved changes will be lost!");
        builder.buildOkButton("Continue");
        builder.buildCancelButton("Cancel");
        return builder.getDialog();
    }
}
```

✅ **Usage Example:**

```java
public class Main {
    public static void main(String[] args) {
        DialogBuilder builder = new AlertDialogBuilder();
        DialogDirector director = new DialogDirector(builder);

        Dialog dialog = director.constructWarningDialog();
        dialog.show();
    }
}
```

**Output:**

```
Dialog: Warning
Message: Unsaved changes will be lost!
[ Continue ] [ Cancel ]
```

---

### 🧠 Flow Summary

| Step | Action                                | Result                       |
| ---- | ------------------------------------- | ---------------------------- |
| 1️⃣  | `DialogDirector` calls builder steps  | Sets title, message, buttons |
| 2️⃣  | `AlertDialogBuilder` builds each part | Creates `Dialog` object      |
| 3️⃣  | `Dialog` returned and displayed       | Fully assembled dialog       |

---

### 🪜 Summary

* Builds complex objects **step by step**.
* **Same construction process** can create different variations (e.g., AlertDialog, InfoDialog).
* Director controls *how* it’s built, Builder controls *what* each part looks like.
* Useful when object creation involves **many optional parameters or configurations**.

---

### 🧾 Real-world Analogy

🍔 **Burger Builder**

* Builder = Chef
* Director = Customer who says “I want a double cheeseburger.”
* Product = Finished burger

Same “build process,” but different ingredients create different results.

---

### 🧭 TL;DR

> **Builder Pattern = Step-by-step construction of complex objects.**
> Separates **how to build** from **what to build**, promoting flexibility and reusability.
> It's like a customizable constructor