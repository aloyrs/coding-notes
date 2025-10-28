# 🧩 State Pattern – Overview

### 🧠 Concept

The **State Pattern** allows an object to **change its behavior** when its **internal state changes**.
It appears as if the object’s **class changes at runtime**.

> 👉 It removes complex `if-else` or `switch` statements for state transitions
> and encapsulates state-specific behavior into separate classes.

---

### 🧱 Key Roles

| Role                  | Description                                                    |
| --------------------- | -------------------------------------------------------------- |
| **Context**           | The main object whose behavior changes depending on its state. |
| **State (Interface)** | Declares methods that represent behavior in a given state.     |
| **ConcreteState**     | Implements behavior specific to a particular state.            |

---

### 💻 Java Example – Report Generator (States: Draft → Review → Published)

```java
// Context
class ReportContext {
    private ReportState state;

    public ReportContext() {
        this.state = new DraftState(); // initial state
    }

    public void setState(ReportState state) {
        this.state = state;
    }

    public void request() {
        state.handle(this);
    }
}

// State interface
interface ReportState {
    void handle(ReportContext context);
}

// Concrete States
class DraftState implements ReportState {
    public void handle(ReportContext context) {
        System.out.println("Report in Draft → Sending for Review...");
        context.setState(new ReviewState());
    }
}

class ReviewState implements ReportState {
    public void handle(ReportContext context) {
        System.out.println("Report under Review → Publishing...");
        context.setState(new PublishedState());
    }
}

class PublishedState implements ReportState {
    public void handle(ReportContext context) {
        System.out.println("Report already Published. No further actions.");
    }
}
```

✅ **Usage Example:**

```java
ReportContext report = new ReportContext();

report.request(); // Draft → Review
report.request(); // Review → Published
report.request(); // Already Published

/*
Output:
Report in Draft → Sending for Review...
Report under Review → Publishing...
Report already Published. No further actions.
*/
```

---

### 🧠 Flow Summary (Step-by-Step)

| Step | Current State | Action      | Next State | Output                                          |
| ---- | ------------- | ----------- | ---------- | ----------------------------------------------- |
| 1️⃣  | Draft         | `request()` | Review     | "Report in Draft → Sending for Review..."       |
| 2️⃣  | Review        | `request()` | Published  | "Report under Review → Publishing..."           |
| 3️⃣  | Published     | `request()` | Published  | "Report already Published. No further actions." |

---

### 🪜 Summary

* Encapsulates **state-specific behavior** into separate classes.
* Eliminates **conditional logic** for state transitions.
* Makes adding new states easier without modifying the core logic.
* Promotes **Open/Closed** and **Single Responsibility** principles.

---

### 📊 Real-world Analogy

📄 **Document Workflow:**
A report changes its behavior as it moves through stages:
**Draft → Review → Published** — each state has its own rules and actions.