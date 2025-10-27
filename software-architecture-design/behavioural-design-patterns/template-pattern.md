### 🧠 Concept

The **Template Method Pattern** defines the **skeleton of a process** in a base class
but lets **subclasses override certain steps** without changing the overall algorithm structure.

> 👉 The base class provides a **template method** that outlines the report generation steps.
> Subclasses fill in the **specific details** (e.g., data source, format).

---

### 🧱 Key Roles

| Role              | Description                                         |
| ----------------- | --------------------------------------------------- |
| **AbstractClass** | Defines the **template method** and abstract steps. |
| **ConcreteClass** | Implements specific details for each report type.   |

---

### 💻 Java Example – Report Generator

```java
// Abstract class (template)
abstract class ReportGenerator {
    // Template method (final – cannot be overridden)
    public final void generateReport() {
        fetchData();
        processData();
        formatReport();
        exportReport();
    }

    // Abstract methods for subclasses to implement
    abstract void fetchData();
    abstract void processData();
    abstract void formatReport();

    // Common method shared by all
    void exportReport() {
        System.out.println("Exporting report to PDF...");
    }
}

// Concrete implementation 1
class SalesReportGenerator extends ReportGenerator {
    void fetchData() { System.out.println("Fetching sales data from database..."); }
    void processData() { System.out.println("Calculating total sales and growth rates..."); }
    void formatReport() { System.out.println("Formatting sales data into summary tables..."); }
}

// Concrete implementation 2
class EmployeeReportGenerator extends ReportGenerator {
    void fetchData() { System.out.println("Retrieving employee records..."); }
    void processData() { System.out.println("Analyzing performance scores..."); }
    void formatReport() { System.out.println("Creating charts and ranking tables..."); }
}
```

✅ **Usage Example:**

```java
ReportGenerator salesReport = new SalesReportGenerator();
salesReport.generateReport();

/*
Fetching sales data from database...
Calculating total sales and growth rates...
Formatting sales data into summary tables...
Exporting report to PDF...
*/

ReportGenerator employeeReport = new EmployeeReportGenerator();
employeeReport.generateReport();

/*
Retrieving employee records...
Analyzing performance scores...
Creating charts and ranking tables...
Exporting report to PDF...
*/
```

---

### 🧠 Flow Summary (Step-by-Step)

| Step | Action           | Base Template Method | Subclass Override | Example Output                         |
| ---- | ---------------- | -------------------- | ----------------- | -------------------------------------- |
| 1️⃣  | `fetchData()`    | —                    | Custom per report | “Fetching sales data from database...” |
| 2️⃣  | `processData()`  | —                    | Custom per report | “Calculating total sales…”             |
| 3️⃣  | `formatReport()` | —                    | Custom per report | “Formatting data into summary tables…” |
| 4️⃣  | `exportReport()` | Common (base class)  | Shared by all     | “Exporting report to PDF…”             |

---

### 🪜 Summary

* Base class defines **the overall workflow** (`generateReport()`).
* Subclasses **fill in details** for individual steps.
* Encourages **code reuse** and **consistent process structure**.
* Follows the **Hollywood Principle** —
  *“Don’t call us, we’ll call you.”* (Base class calls subclass methods.)

---

### 📊 Real-world Analogy

🧾 **Report Templates in BI Tools** —
Every report follows the same process:
**Fetch → Process → Format → Export**,
but each report type defines **its own implementation** for each step.
