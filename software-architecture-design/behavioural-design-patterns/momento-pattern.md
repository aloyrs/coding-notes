### **Definition**

> The **Memento Pattern** captures and externalizes an object’s **internal state** without violating encapsulation — so that the object can be **restored** to that state later.

---

### **Purpose**

* Allows **undo / redo** functionality.
* Keeps state snapshots **without exposing** object internals.

---

### **Key Roles**

| Role           | Description                                          |
| -------------- | ---------------------------------------------------- |
| **Originator** | The object whose state you want to save and restore. |
| **Memento**    | Stores the state of the Originator.                  |
| **Caretaker**  | Manages Memento objects (e.g., saving, restoring).   |

---

### **Java Example**

```java
// Memento: stores state
class EditorMemento {
    private final String content;
    EditorMemento(String content) { this.content = content; }
    String getContent() { return content; }
}

// Originator: creates/restores mementos
class Editor {
    private String content = "";
    void type(String words) { content += words; }
    String getContent() { return content; }

    EditorMemento save() { return new EditorMemento(content); }
    void restore(EditorMemento memento) { content = memento.getContent(); }
}

// Caretaker: manages mementos
class History {
    private final Stack<EditorMemento> history = new Stack<>();
    void save(Editor editor) { history.push(editor.save()); }
    void undo(Editor editor) {
        if (!history.isEmpty()) editor.restore(history.pop());
    }
}
```

✅ **Usage Example:**

```java
Editor editor = new Editor();
History history = new History();

editor.type("Hello ");
history.save(editor);

editor.type("World!");
history.save(editor);

editor.type(" Extra text...");
history.undo(editor);

System.out.println(editor.getContent()); // "Hello World!"
```

---

### **Pros ✅**

* Supports **undo/rollback** easily.
* Preserves **encapsulation** (no direct access to internals).

### **Cons ❌**

* Can use **lots of memory** if many states are stored.
* Must manage **memento history carefully**.

---

### **Real-world Analogy**

📝 Like using **Ctrl + Z** in a text editor — the system saves snapshots of your text so you can go back to a previous version.