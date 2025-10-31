# 🧩 Proxy Pattern – Overview

### 🧠 Concept

The **Proxy Pattern** provides a **substitute or placeholder** for another object
to control access to it — like adding a _gatekeeper_ in front of a real service.

> 💡 Think of it as a **middleman** that decides _when and how_ to talk to the real object.

---

### 🧱 Key Roles

| Role            | Description                                                                              |
| --------------- | ---------------------------------------------------------------------------------------- |
| **Subject**     | Common interface for RealSubject and Proxy.                                              |
| **RealSubject** | The actual object that performs the real work.                                           |
| **Proxy**       | Controls access to the RealSubject (e.g., for caching, logging, security, etc.).         |
| **Client**      | Uses the Subject interface — unaware whether it’s talking to a Proxy or the real object. |

---

### 💻 Java Example – Image Loading Example

```java
// ----- Subject -----
interface Image {
    void display();
}

// ----- Real Subject -----
class RealImage implements Image {
    private String filename;

    public RealImage(String filename) {
        this.filename = filename;
        loadFromDisk();
    }

    private void loadFromDisk() {
        System.out.println("Loading image from disk: " + filename);
    }

    public void display() {
        System.out.println("Displaying: " + filename);
    }
}

// ----- Proxy -----
class ProxyImage implements Image {
    private String filename;
    private RealImage realImage;

    public ProxyImage(String filename) {
        this.filename = filename;
    }

    public void display() {
        // Lazy loading — only load when needed
        if (realImage == null) {
            realImage = new RealImage(filename);
        }
        realImage.display();
    }
}

// ----- Client -----
public class Main {
    public static void main(String[] args) {
        Image image = new ProxyImage("photo.png");

        // Image not loaded yet
        System.out.println("First display:");
        image.display();

        // Cached object used (no reload)
        System.out.println("\nSecond display:");
        image.display();
    }
}
```

**Output:**

```
First display:
Loading image from disk: photo.png
Displaying: photo.png

Second display:
Displaying: photo.png
```

---

### 🧠 Flow Summary

| Step | Action                        | Behavior                              |
| ---- | ----------------------------- | ------------------------------------- |
| 1️⃣   | Client creates `ProxyImage`   | No actual image loaded yet            |
| 2️⃣   | `display()` called first time | Proxy loads `RealImage` from disk     |
| 3️⃣   | `display()` called again      | Proxy reuses the cached image         |
| ✅   | Result                        | Same interface, optimized performance |

---

### 🪜 Summary

- Controls access to the real object (lazy loading, logging, access control, etc.)
- Keeps client code unaware of whether it’s using the real object or a proxy.
- Commonly used for:

  - 🖼️ **Virtual Proxy** → lazy initialization (like image example)
  - 🔐 **Protection Proxy** → access control
  - 🗂️ **Remote Proxy** → communication with remote services
  - 💾 **Caching Proxy** → caching expensive operations

---

### 🧾 Real-world Analogy

🛡️ **Security Guard (Proxy)**

- A guard checks your ID before letting you meet the CEO (RealSubject).
- The CEO doesn’t deal with everyone directly — the guard (Proxy) controls access.

💡 The guard and CEO both implement “meet” behavior, but the guard adds control.

---

### 🧭 TL;DR

> **Proxy Pattern = Acts as a stand-in for another object to control access.**
> “Same interface, extra control — without changing the real object.”
