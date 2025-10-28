# 🔒 Singleton Pattern – Overview

### 🧠 Concept

The **Singleton Pattern** ensures that **only one instance** of a class exists
and provides a **global point of access** to it.

> 👉 Useful when you need a single, shared resource (e.g., configuration, logger, connection pool).

---

### 🧱 Key Points

| Concept                 | Description                                              |
| ----------------------- | -------------------------------------------------------- |
| **Single Instance**     | Only one object of the class is created.                 |
| **Global Access Point** | Instance is accessible globally through a static method. |
| **Private Constructor** | Prevents direct instantiation from outside.              |

---

### 💻 Java Example – Logger Singleton

```java
public class Logger {
    // Step 1: Create a private static instance
    private static Logger instance;

    // Step 2: Make constructor private
    private Logger() {
        System.out.println("Logger initialized");
    }

    // Step 3: Provide a global access method
    public static Logger getInstance() {
        if (instance == null) {
            instance = new Logger(); // lazy initialization
        }
        return instance;
    }

    public void log(String message) {
        System.out.println("[LOG] " + message);
    }
}
```

✅ **Usage Example:**

```java
Logger log1 = Logger.getInstance();
Logger log2 = Logger.getInstance();

log1.log("Starting system...");
log2.log("System running...");

System.out.println(log1 == log2); // true → same instance
```

**Output:**

```
Logger initialized
[LOG] Starting system...
[LOG] System running...
true
```

---

### 🧠 Flow Summary (Step-by-Step)

| Step | Action                 | Instance State                   | Output                  |
| ---- | ---------------------- | -------------------------------- | ----------------------- |
| 1️⃣  | First `getInstance()`  | Creates new Logger               | “Logger initialized”    |
| 2️⃣  | Second `getInstance()` | Returns existing instance        | Same object used        |
| 3️⃣  | `log()` calls          | Work on the same shared instance | “Starting system…” etc. |

---

### 🪜 Summary

* Ensures **only one object** exists for the whole app.
* Provides **controlled access** to that object.
* Saves memory by **sharing** one instance.
* Commonly used for:

  * Logging
  * Configuration managers
  * Database connection pools

---

### ⚙️ Thread-safe Singleton (Improved)

```java
public class Logger {
    private static volatile Logger instance;

    private Logger() {}

    public static Logger getInstance() {
        if (instance == null) {
            synchronized (Logger.class) {
                if (instance == null) {
                    instance = new Logger();
                }
            }
        }
        return instance;
    }
}
```

✅ **Double-checked locking** ensures thread safety with minimal synchronization overhead.

---

### 📦 Real-world Analogy

🏢 **Company CEO**
There can be **only one CEO** in a company.
Everyone accesses decisions **through that one person** — not by creating new CEOs.

---

### 🧭 TL;DR

> **Singleton = One Object to Rule Them All**
> Ensures only one instance exists and provides a global access point.