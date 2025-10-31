# 🔌 Adapter Pattern – Overview

### 🧠 Concept

The **Adapter Pattern** allows **incompatible interfaces to work together**
by providing a **wrapper (adapter)** that translates one interface into another.

> 💡 Think of it as a _power plug converter_ — it adapts one type of plug to fit another socket.

---

### 🧱 Key Roles

| Role        | Description                                                               |
| ----------- | ------------------------------------------------------------------------- |
| **Target**  | The expected interface (what the client uses).                            |
| **Adaptee** | The existing class with an incompatible interface.                        |
| **Adapter** | Wraps the Adaptee and translates its interface into the Target’s format.  |
| **Client**  | Uses the Target interface — unaware of the adapter’s internal conversion. |

---

### 💻 Java Example – UI Example (Modern vs Legacy Buttons)

```java
// ----- Target Interface -----
interface Button {
    void click();
}

// ----- Adaptee -----
class LegacyButton {
    public void onPress() {
        System.out.println("Legacy button pressed!");
    }
}

// ----- Adapter -----
class ButtonAdapter implements Button {
    private LegacyButton legacyButton;

    public ButtonAdapter(LegacyButton legacyButton) {
        this.legacyButton = legacyButton;
    }

    @Override
    public void click() {
        // Adapt click() call to legacy onPress() method
        legacyButton.onPress();
    }
}

// ----- Client -----
public class Main {
    public static void main(String[] args) {
        Button newButton = new ButtonAdapter(new LegacyButton());
        newButton.click();  // Client uses Target interface
    }
}
```

**Output:**

```
Legacy button pressed!
```

---

### 🧠 Flow Summary

| Step | Action                                     | Adapter Does              |
| ---- | ------------------------------------------ | ------------------------- |
| 1️⃣   | Client calls `click()`                     | Adapter receives the call |
| 2️⃣   | Adapter translates `click()` → `onPress()` | Calls legacy method       |
| 3️⃣   | Adaptee (`LegacyButton`) executes normally | Works seamlessly          |

---

### 🪜 Summary

- Converts **one interface to another** that the client expects.
- Enables reuse of **existing (legacy)** classes with new systems.
- Promotes **open/closed principle** — extend behavior without modifying existing code.
- Can be implemented via **object composition** (preferred) or **class inheritance**.

---

### 🧾 Real-world Analogy

🔌 **Power Adapter**

- Laptop (client) expects a **USB-C** plug (Target).
- Wall outlet has **Type G** plug (Adaptee).
- **Adapter** converts between them so they can connect.

💡 The devices stay unchanged — only the adapter bridges them.

---

### 🧭 TL;DR

> **Adapter Pattern = Translator between incompatible interfaces.**
> “Make old code talk to new code — without changing either.”
