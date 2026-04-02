# 🏭 Factory Pattern

### 🧠 Concept

The **Factory Pattern** is a **creational design pattern** that provides an interface
for **creating objects**, but **lets subclasses decide** which class to instantiate.

> 👉 It **encapsulates object creation logic**, making your code more flexible and maintainable.

---

### 🧱 Key Roles

| Role                    | Description                                                |
| ----------------------- | ---------------------------------------------------------- |
| **Product (Interface)** | Defines the common interface for all objects created.      |
| **ConcreteProduct**     | Actual implementation of the product.                      |
| **Creator (Factory)**   | Declares the factory method that returns Product objects.  |
| **ConcreteCreator**     | Implements the factory method to create specific products. |

---

### 💻 Java Example – Report Generator Factory

```java
// Product interface
interface Report {
    void generate();
}

// Concrete products
class PDFReport implements Report {
    public void generate() {
        System.out.println("Generating PDF report...");
    }
}

class ExcelReport implements Report {
    public void generate() {
        System.out.println("Generating Excel report...");
    }
}

// Factory class
class ReportFactory {
    public static Report createReport(String type) {
        switch (type) {
            case "PDF": return new PDFReport();
            case "EXCEL": return new ExcelReport();
            default: throw new IllegalArgumentException("Unknown report type");
        }
    }
}
```

✅ **Usage Example:**

```java
Report pdf = ReportFactory.createReport("PDF");
pdf.generate();

Report excel = ReportFactory.createReport("EXCEL");
excel.generate();
```

**Output:**

```
Generating PDF report...
Generating Excel report...
```

---

### 🧠 Flow Summary (Step-by-Step)

| Step | Action                  | Factory Role                  | Output                       |
| ---- | ----------------------- | ----------------------------- | ---------------------------- |
| 1️⃣  | `createReport("PDF")`   | Creates a PDFReport object    | “Generating PDF report...”   |
| 2️⃣  | `createReport("EXCEL")` | Creates an ExcelReport object | “Generating Excel report...” |

💬 **Note:** The client never knows which concrete class is used — just the interface.

---

### 🪜 Summary

* **Encapsulates object creation**, hiding logic from the client.
* Makes it easy to **add new product types** without changing existing code.
* Reduces **tight coupling** between client and concrete classes.
* Promotes **Open/Closed Principle** (open for extension, closed for modification).

---

### 🧰 Variants

| Variant              | Description                                                 |
| -------------------- | ----------------------------------------------------------- |
| **Simple Factory**   | Uses a single static method to create objects (like above). |
| **Factory Method**   | Uses inheritance; subclasses decide which object to create. |
| **Abstract Factory** | Creates **families** of related objects.                    |

---

### 🧾 Real-world Analogy

🖨️ **Document Export Tool**
You click “Export” → choose **PDF**, **Excel**, or **Word**.
The app uses a **factory** to create the correct exporter automatically —
you just get the right output without worrying about how it’s built.

---

### 🧭 TL;DR

> **Factory Pattern = Smart Object Creator**
> It hides object creation details and makes your code flexible and scalable.

> The client doesn’t create objects directly — the factory handles object creation.