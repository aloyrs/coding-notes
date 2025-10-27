### 🧩 Concept

The **Observer Pattern** defines a **one-to-many relationship** between objects,
so that when **one object changes state (Subject)**,
**all its dependents (Observers)** are **notified automatically**.

---

### 🧠 Key Roles

| Role                 | Description                                         |
| -------------------- | --------------------------------------------------- |
| **Subject**          | Holds data/state and maintains a list of observers. |
| **Observer**         | Gets notified when the subject changes.             |
| **ConcreteSubject**  | Actual object being observed.                       |
| **ConcreteObserver** | Responds to updates from the subject.               |

---

### 💻 Simple Java Example

```java
// Observer interface
interface Observer {
    void update(String news);
}

// Subject class
class NewsAgency {
    private List<Observer> observers = new ArrayList<>();
    private String news;

    void addObserver(Observer o) { observers.add(o); }
    void removeObserver(Observer o) { observers.remove(o); }

    void setNews(String news) {
        this.news = news;
        notifyObservers();
    }

    private void notifyObservers() {
        for (Observer o : observers) o.update(news);
    }
}

// Concrete observer
class NewsChannel implements Observer {
    private String news;
    public void update(String news) { this.news = news; }
}
```

✅ **Usage Example:**

```java
NewsAgency agency = new NewsAgency();
NewsChannel channel1 = new NewsChannel();
NewsChannel channel2 = new NewsChannel();

agency.addObserver(channel1);
agency.addObserver(channel2);

agency.setNews("Breaking: New Java Release!");
// Both channel1 and channel2 receive update
```

---

### 🧱 Flow Summary (Step-by-Step)

| Step | Action                   | Subject (NewsAgency) | Observers                  | Notes                  |
| ---- | ------------------------ | -------------------- | -------------------------- | ---------------------- |
| 1️⃣  | addObserver(channel1)    | [channel1]           | —                          | Register observer      |
| 2️⃣  | addObserver(channel2)    | [channel1, channel2] | —                          | Register another       |
| 3️⃣  | setNews("Breaking...")   | Notifies both        | channel1, channel2 updated | Trigger update         |
| 4️⃣  | removeObserver(channel2) | [channel1]           | channel2 removed           | Stop receiving updates |

---

### 🪜 Summary

* **Subject** → keeps track of observers
* **Observers** → automatically get updates
* **Loose coupling** → Subject doesn’t need to know concrete observer types
* Common use cases: **UI listeners, event systems, notifications**

---

### 🔔 Real-world Analogy

📰 **News Agency & Subscribers** — when the agency publishes news,
all subscribed channels automatically receive it.
