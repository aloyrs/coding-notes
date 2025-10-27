### **S – Single Responsibility Principle (SRP)**

> A class should have **only one reason to change**.
> ➡ Do **one thing well**.

```java
class ReportPrinter {
    void print(Report report) { /* printing logic */ }
}
class ReportSaver {
    void save(Report report) { /* saving logic */ }
}
```

✅ Each class has a single job — printing or saving.

---

### **O – Open/Closed Principle (OCP)**

> Classes should be **open for extension**, but **closed for modification**.
> ➡ Extend behavior without changing existing code.

```java
interface Discount {
    double apply(double price);
}
class ChristmasDiscount implements Discount {
    public double apply(double price) { return price * 0.8; }
}
```

✅ Add new discounts by creating new classes, not editing old ones.

---

### **L – Liskov Substitution Principle (LSP)**

> Subclasses should be **replaceable** by their base classes.
> ➡ Child class must **honor parent behavior**.

```java
class Bird { void fly() {} }
class Sparrow extends Bird { /* ok */ }
// class Ostrich extends Bird { void fly() { throw new UnsupportedOperationException(); } } ❌ violates LSP
```

✅ All subclasses must behave consistently with the base class.

---

### **I – Interface Segregation Principle (ISP)**

> Clients shouldn’t depend on **methods they don’t use**.
> ➡ Use **small, specific interfaces**.

```java
interface Printer { void print(); }
interface Scanner { void scan(); }

class AllInOnePrinter implements Printer, Scanner { /* ... */ }
class SimplePrinter implements Printer { /* ... */ }
```

✅ Classes implement only what they need.

---

### **D – Dependency Inversion Principle (DIP)**

> Depend on **abstractions**, not **concrete classes**.
> ➡ High-level modules shouldn’t depend on low-level details.

```java
interface MessageSender { void send(String msg); }
class EmailSender implements MessageSender { public void send(String msg) { /* ... */ } }

class NotificationService {
    private final MessageSender sender;
    NotificationService(MessageSender sender) { this.sender = sender; }
}
```

✅ Swap dependencies (e.g., `EmailSender`, `SmsSender`) without changing core logic.
