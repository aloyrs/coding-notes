# 🏢 Abstract Factory Pattern – Overview

### 🧠 Concept

The **Abstract Factory Pattern** provides an interface for creating **families of related objects**
**without specifying their concrete classes**.

> 👉 It’s like a “**factory of factories**” — it groups individual factories that produce related objects.

---

### 🧱 Key Roles

| Role                | Description                                                               |
| ------------------- | ------------------------------------------------------------------------- |
| **AbstractFactory** | Declares methods for creating abstract products.                          |
| **ConcreteFactory** | Implements creation methods for a specific product family.                |
| **AbstractProduct** | Common interface for a product type.                                      |
| **ConcreteProduct** | Specific implementation of a product.                                     |
| **Client**          | Uses the factory to create products — without knowing the actual classes. |

---

### 💻 Java Example – Report Generator Suite

*(Each factory creates related report components: Header + Body)*

```java
// Abstract Products
interface ReportHeader { void printHeader(); }
interface ReportBody { void printBody(); }

// Concrete Products (PDF)
class PDFReportHeader implements ReportHeader {
    public void printHeader() { System.out.println("PDF Report Header"); }
}
class PDFReportBody implements ReportBody {
    public void printBody() { System.out.println("PDF Report Body"); }
}

// Concrete Products (Excel)
class ExcelReportHeader implements ReportHeader {
    public void printHeader() { System.out.println("Excel Report Header"); }
}
class ExcelReportBody implements ReportBody {
    public void printBody() { System.out.println("Excel Report Body"); }
}

// Abstract Factory
interface ReportFactory {
    ReportHeader createHeader();
    ReportBody createBody();
}

// Concrete Factories
class PDFReportFactory implements ReportFactory {
    public ReportHeader createHeader() { return new PDFReportHeader(); }
    public ReportBody createBody() { return new PDFReportBody(); }
}

class ExcelReportFactory implements ReportFactory {
    public ReportHeader createHeader() { return new ExcelReportHeader(); }
    public ReportBody createBody() { return new ExcelReportBody(); }
}

// Client
class ReportApplication {
    private ReportHeader header;
    private ReportBody body;

    public ReportApplication(ReportFactory factory) {
        header = factory.createHeader();
        body = factory.createBody();
    }

    public void printReport() {
        header.printHeader();
        body.printBody();
    }
}
```

✅ **Usage Example:**

```java
ReportFactory pdfFactory = new PDFReportFactory();
ReportApplication pdfReport = new ReportApplication(pdfFactory);
pdfReport.printReport();

ReportFactory excelFactory = new ExcelReportFactory();
ReportApplication excelReport = new ReportApplication(excelFactory);
excelReport.printReport();
```

**Output:**

```
PDF Report Header
PDF Report Body
Excel Report Header
Excel Report Body
```

---

### 🧠 Flow Summary (Step-by-Step)

| Step | Action                     | Factory Used             | Output                       |
| ---- | -------------------------- | ------------------------ | ---------------------------- |
| 1️⃣  | `new PDFReportFactory()`   | Creates PDF components   | “PDF Report Header / Body”   |
| 2️⃣  | `new ExcelReportFactory()` | Creates Excel components | “Excel Report Header / Body” |

💬 **Note:** The client never knows about the specific classes —
it only interacts with the abstract `ReportFactory` interface.

---

### 🪜 Summary

* Creates **families of related objects** (e.g., PDF or Excel components).
* Keeps creation logic centralized in factories.
* Client code remains **decoupled** from concrete implementations.
* Promotes **Open/Closed Principle** — new product families can be added easily.
* Builds on the **Factory Method Pattern** by grouping related factories.

---

### 🧾 Real-world Analogy

🖥️ **UI Theme Factory**
Each theme (Light/Dark) creates consistent **sets of UI components**:

* LightThemeFactory → LightButton, LightTextField
* DarkThemeFactory → DarkButton, DarkTextField

💡 The app just picks a factory (theme) — and gets all matching components.

---

### 🧭 TL;DR

> **Abstract Factory = Factory of Factories**
> Creates groups of related objects without exposing their concrete classes.