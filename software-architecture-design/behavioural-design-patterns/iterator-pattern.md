### 🧠 Concept

The **Iterator Pattern** provides a way to **access elements of a collection sequentially**
**without exposing** the collection’s internal structure.

> 👉 It separates **traversal logic** from the **collection itself**,
> allowing flexible iteration across different types of collections.

---

### 🧱 Key Roles

| Role                       | Description                                                   |
| -------------------------- | ------------------------------------------------------------- |
| **Iterator**               | Interface defining traversal methods (`hasNext()`, `next()`). |
| **ConcreteIterator**       | Implements the actual iteration logic.                        |
| **Aggregate (Collection)** | Interface defining a method to create an iterator.            |
| **ConcreteAggregate**      | Implements the collection and provides its iterator.          |

---

### 💻 Java Example – Report Iterator

```java
// Iterator interface
interface Iterator<T> {
    boolean hasNext();
    T next();
}

// Aggregate interface
interface ReportCollection {
    Iterator<String> createIterator();
}

// Concrete collection
class ReportList implements ReportCollection {
    private List<String> reports = new ArrayList<>();

    void addReport(String report) {
        reports.add(report);
    }

    public Iterator<String> createIterator() {
        return new ReportIterator(reports);
    }
}

// Concrete iterator
class ReportIterator implements Iterator<String> {
    private List<String> reports;
    private int index = 0;

    ReportIterator(List<String> reports) {
        this.reports = reports;
    }

    public boolean hasNext() {
        return index < reports.size();
    }

    public String next() {
        return hasNext() ? reports.get(index++) : null;
    }
}
```

✅ **Usage Example:**

```java
ReportList reportList = new ReportList();
reportList.addReport("Sales Report");
reportList.addReport("Employee Report");
reportList.addReport("Inventory Report");

Iterator<String> iterator = reportList.createIterator();

while (iterator.hasNext()) {
    System.out.println(iterator.next());
}

/*
Sales Report
Employee Report
Inventory Report
*/
```

---

### 🧠 Flow Summary (Step-by-Step)

| Step | Action              | Iterator State | Output             |
| ---- | ------------------- | -------------- | ------------------ |
| 1️⃣  | `createIterator()`  | index = 0      | —                  |
| 2️⃣  | `hasNext()` → true  | index = 0      | —                  |
| 3️⃣  | `next()`            | index = 1      | "Sales Report"     |
| 4️⃣  | `next()`            | index = 2      | "Employee Report"  |
| 5️⃣  | `next()`            | index = 3      | "Inventory Report" |
| 6️⃣  | `hasNext()` → false | —              | Iteration ends     |

---

### 🪜 Summary

* Provides a **uniform interface** to traverse different collections.
* **Encapsulates iteration logic** inside a separate object.
* Allows multiple iterators on the same collection.
* Promotes **Single Responsibility** and **Open/Closed Principles**.

---

### 📊 Real-world Analogy

📚 **Book Shelf Iterator** –
You can go through books **one by one** using the same method (`next()`),
without knowing **how** they’re stored (array, list, or database).