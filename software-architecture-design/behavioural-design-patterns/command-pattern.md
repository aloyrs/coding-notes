### 🧩 Concept

The **Command Pattern** turns a **request or action into an object**.
This lets you **parameterize**, **queue**, **log**, or **undo** actions easily.

> 👉 It decouples the **object that issues a request (Invoker)**
> from the **object that performs it (Receiver)**.

---

### 🧱 Key Roles

| Role                    | Description                                             |
| ----------------------- | ------------------------------------------------------- |
| **Command (Interface)** | Declares an `execute()` method.                         |
| **ConcreteCommand**     | Implements `execute()` and calls the receiver’s method. |
| **Receiver**            | Knows how to perform the actual operation.              |
| **Invoker**             | Triggers the command’s execution.                       |
| **Client**              | Configures commands and assigns them to the invoker.    |

---

### 💻 Simple Java Example

```java
// Command interface
interface Command {
    void execute();
}

// Receiver
class Light {
    void turnOn() { System.out.println("Light is ON"); }
    void turnOff() { System.out.println("Light is OFF"); }
}

// Concrete commands
class TurnOnCommand implements Command {
    private Light light;
    TurnOnCommand(Light light) { this.light = light; }
    public void execute() { light.turnOn(); }
}

class TurnOffCommand implements Command {
    private Light light;
    TurnOffCommand(Light light) { this.light = light; }
    public void execute() { light.turnOff(); }
}

// Invoker
class RemoteControl {
    private Command command;
    void setCommand(Command command) { this.command = command; }
    void pressButton() { command.execute(); }
}
```

✅ **Usage Example:**

```java
Light light = new Light();
RemoteControl remote = new RemoteControl();

remote.setCommand(new TurnOnCommand(light));
remote.pressButton();  // Light is ON

remote.setCommand(new TurnOffCommand(light));
remote.pressButton();  // Light is OFF
```

---

### 🧠 Flow Summary (Step-by-Step)

| Step | Action                     | Invoker (Remote)      | Command                          | Receiver (Light) | Output |
| ---- | -------------------------- | --------------------- | -------------------------------- | ---------------- | ------ |
| 1️⃣  | setCommand(TurnOnCommand)  | stores TurnOnCommand  | TurnOnCommand                    | —                | —      |
| 2️⃣  | pressButton()              | executes command      | TurnOnCommand → light.turnOn()   | "Light is ON"    |        |
| 3️⃣  | setCommand(TurnOffCommand) | stores TurnOffCommand | TurnOffCommand                   | —                | —      |
| 4️⃣  | pressButton()              | executes command      | TurnOffCommand → light.turnOff() | "Light is OFF"   |        |

---

### 🪜 Summary

* Encapsulates **actions as objects**.
* Allows **undo**, **redo**, **macro**, or **queue** of commands.
* Promotes **loose coupling** between **Invoker** and **Receiver**.
* Useful for **UI buttons, transactions, task scheduling**.

---

### 💡 Real-world Analogy

🎮 **Remote Control** — each button (Invoker) is linked to a command (e.g., TurnOnCommand),
which tells the **device (Receiver)** what to do.