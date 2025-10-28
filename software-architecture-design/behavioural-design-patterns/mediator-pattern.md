# 🧭 Mediator Pattern – Overview

### 🧠 Concept

The **Mediator Pattern** defines an object (**Mediator**) that **centralizes communication** between multiple objects (called **Colleagues**) so they don’t talk to each other directly.

> 👉 Promotes **loose coupling** by preventing classes from referring to each other explicitly.

---

### 🧱 Key Roles

| Role                  | Description                                                    |
| --------------------- | -------------------------------------------------------------- |
| **Mediator**          | Defines how objects (colleagues) interact.                     |
| **ConcreteMediator**  | Implements communication logic between colleagues.             |
| **Colleague**         | Components that communicate through the mediator.              |
| **ConcreteColleague** | Actual components that send/receive messages via the mediator. |

---

### 💻 Java Example – Chat Room (Mediator)

```java
// Mediator interface
interface ChatMediator {
    void sendMessage(String message, User sender);
    void addUser(User user);
}

// Concrete Mediator
class ChatRoom implements ChatMediator {
    private List<User> users = new ArrayList<>();

    public void addUser(User user) {
        users.add(user);
    }

    public void sendMessage(String message, User sender) {
        for (User user : users) {
            if (user != sender) {
                user.receive(message);
            }
        }
    }
}

// Colleague
abstract class User {
    protected ChatMediator mediator;
    protected String name;

    public User(ChatMediator mediator, String name) {
        this.mediator = mediator;
        this.name = name;
    }

    abstract void send(String message);
    abstract void receive(String message);
}

// Concrete Colleague
class ChatUser extends User {
    public ChatUser(ChatMediator mediator, String name) {
        super(mediator, name);
    }

    void send(String message) {
        System.out.println(name + " sends: " + message);
        mediator.sendMessage(message, this);
    }

    void receive(String message) {
        System.out.println(name + " receives: " + message);
    }
}
```

✅ **Usage Example:**

```java
ChatMediator chat = new ChatRoom();

User alice = new ChatUser(chat, "Alice");
User bob = new ChatUser(chat, "Bob");
User charlie = new ChatUser(chat, "Charlie");

chat.addUser(alice);
chat.addUser(bob);
chat.addUser(charlie);

alice.send("Hi everyone!");
bob.send("Hello Alice!");
```

**Output:**

```
Alice sends: Hi everyone!
Bob receives: Hi everyone!
Charlie receives: Hi everyone!

Bob sends: Hello Alice!
Alice receives: Hello Alice!
Charlie receives: Hello Alice!
```

---

### 🧠 Flow Summary (Step-by-Step)

| Step | Action              | Mediator Role             | Output                  |
| ---- | ------------------- | ------------------------- | ----------------------- |
| 1️⃣  | `Alice.send("Hi")`  | Mediator forwards message | Bob + Charlie receive   |
| 2️⃣  | `Bob.send("Hello")` | Mediator forwards message | Alice + Charlie receive |

💬 **Note:** Alice and Bob don’t know each other directly — they only know the `ChatRoom`.

---

### 🪜 Summary

* Centralizes communication logic → reduces dependencies between objects.
* Each object only depends on the **Mediator**, not on other objects.
* Easier to add new participants without changing existing ones.
* Promotes **loose coupling** and **single responsibility**.

---

### 📡 Real-world Analogy

🗣️ **Group Chat / Air Traffic Control**

* In a **chat room**, users don’t message each other directly —
  messages go through the **chat server (mediator)**.
* In **air traffic control**, planes (colleagues) don’t talk to each other —
  they communicate only through the **control tower (mediator)**.

---

### 🧭 TL;DR

> **Mediator Pattern = Communication Hub**
> Objects stop talking directly and instead talk through one central mediator.