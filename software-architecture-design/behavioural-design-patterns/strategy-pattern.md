### 🧠 Concept

The **Strategy Pattern** defines a family of algorithms,
encapsulates each one, and makes them **interchangeable**.
This lets you **change behavior at runtime** without modifying the context class.

---

### 🧱 Key Roles

| Role                     | Description                                                           |
| ------------------------ | --------------------------------------------------------------------- |
| **Strategy (Interface)** | Defines a common behavior (algorithm contract).                       |
| **ConcreteStrategy**     | Implements a specific algorithm.                                      |
| **Context**              | Uses a `Strategy` to perform a task; can swap strategies dynamically. |

---

### 💻 Simple Java Example

```java
// Strategy interface
interface PaymentStrategy {
    void pay(int amount);
}

// Concrete strategies
class CreditCardPayment implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using Credit Card.");
    }
}

class PayPalPayment implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using PayPal.");
    }
}

// Context
class ShoppingCart {
    private PaymentStrategy strategy;

    void setPaymentStrategy(PaymentStrategy strategy) {
        this.strategy = strategy;
    }

    void checkout(int amount) {
        strategy.pay(amount);
    }
}
```

✅ **Usage Example:**

```java
ShoppingCart cart = new ShoppingCart();

cart.setPaymentStrategy(new CreditCardPayment());
cart.checkout(100);  // Paid 100 using Credit Card.

cart.setPaymentStrategy(new PayPalPayment());
cart.checkout(200);  // Paid 200 using PayPal.
```

---

### ⚙️ Flow Summary (Step-by-Step)

| Step | Action                         | Context (`ShoppingCart`) | Strategy Used     | Output                        |
| ---- | ------------------------------ | ------------------------ | ----------------- | ----------------------------- |
| 1️⃣  | setPaymentStrategy(CreditCard) | CreditCardPayment        | CreditCardPayment | —                             |
| 2️⃣  | checkout(100)                  | → calls `pay(100)`       | CreditCardPayment | "Paid 100 using Credit Card." |
| 3️⃣  | setPaymentStrategy(PayPal)     | PayPalPayment            | PayPalPayment     | —                             |
| 4️⃣  | checkout(200)                  | → calls `pay(200)`       | PayPalPayment     | "Paid 200 using PayPal."      |

---

### 🪜 Summary

* **Encapsulates** different algorithms behind a common interface.
* **Context** delegates behavior to the chosen **Strategy**.
* Easy to **add new behaviors** without touching existing code.
* Promotes **Open/Closed Principle (OCP)**.

---

### 🎯 Real-world Analogy

💳 **Payment Methods** – You can choose to pay by **Credit Card**, **PayPal**, or **Cash**,
but the **checkout process** stays the same.