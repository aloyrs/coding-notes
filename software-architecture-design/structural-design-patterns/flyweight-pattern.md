# 🪶 Flyweight Pattern – Overview

### 🧠 Concept

The **Flyweight Pattern** minimizes **memory usage** by **sharing common data** between similar objects.
It separates **intrinsic (shared)** and **extrinsic (unique)** state so that many objects can reuse the same shared data.

> 💡 Think of it like a **font rendering system** — each letter “A” on screen doesn’t create a new font shape;
> it **reuses** the same letter glyph, only changing position and color.

---

### 🧱 Key Roles

| Role                   | Description                                                         |
| ---------------------- | ------------------------------------------------------------------- |
| **Flyweight**          | Defines an interface for objects that can share intrinsic data.     |
| **Concrete Flyweight** | Implements the shared part of the object.                           |
| **Flyweight Factory**  | Creates and manages shared flyweight instances.                     |
| **Client**             | Uses flyweights and supplies external (extrinsic) data when needed. |

---

### 💻 Java Example – Drawing Trees in a Game

```java
import java.util.*;

// ----- Flyweight -----
interface TreeType {
    void draw(int x, int y);
}

// ----- Concrete Flyweight -----
class ConcreteTreeType implements TreeType {
    private final String name;   // intrinsic state
    private final String color;
    private final String texture;

    public ConcreteTreeType(String name, String color, String texture) {
        this.name = name;
        this.color = color;
        this.texture = texture;
    }

    @Override
    public void draw(int x, int y) {
        System.out.println("Drawing " + name + " tree (" + color + ", " + texture + ") at (" + x + "," + y + ")");
    }
}

// ----- Flyweight Factory -----
class TreeFactory {
    private static final Map<String, TreeType> treeTypes = new HashMap<>();

    public static TreeType getTreeType(String name, String color, String texture) {
        String key = name + color + texture;
        treeTypes.putIfAbsent(key, new ConcreteTreeType(name, color, texture));
        return treeTypes.get(key);
    }
}

// ----- Context / Client -----
class Tree {
    private final int x;   // extrinsic state
    private final int y;
    private final TreeType type;  // shared flyweight

    public Tree(int x, int y, TreeType type) {
        this.x = x;
        this.y = y;
        this.type = type;
    }

    public void draw() {
        type.draw(x, y);
    }
}

public class Main {
    public static void main(String[] args) {
        TreeType oakType = TreeFactory.getTreeType("Oak", "Green", "Rough");
        TreeType pineType = TreeFactory.getTreeType("Pine", "DarkGreen", "Smooth");

        List<Tree> forest = List.of(
            new Tree(10, 20, oakType),
            new Tree(15, 25, oakType),
            new Tree(50, 60, pineType)
        );

        forest.forEach(Tree::draw);
    }
}
```

**Output:**

```
Drawing Oak tree (Green, Rough) at (10,20)
Drawing Oak tree (Green, Rough) at (15,25)
Drawing Pine tree (DarkGreen, Smooth) at (50,60)
```

---

### 🧠 Flow Summary

| Step | Action                               | Result                                      |
| ---- | ------------------------------------ | ------------------------------------------- |
| 1️⃣   | Factory checks if a tree type exists | If yes → reuse; If no → create new          |
| 2️⃣   | Client creates many Tree objects     | Each has unique (x,y) but shared `TreeType` |
| 3️⃣   | Trees draw themselves                | Shared intrinsic data reused to save memory |

---

### 🪜 Summary

- Reduces **RAM usage** when there are **many similar objects**.
- Shares **intrinsic (common)** state, stores **extrinsic (unique)** state externally.
- Best for **performance optimization** in large systems (e.g., graphics, text editors, games).
- Often combined with **Factory Pattern** to manage object creation.

---

### 🧾 Real-world Analogy

🌲 **Forest Rendering**

- You draw **thousands of trees**, but they all share the same model, color, and texture.
- Only their positions differ.
- The shared tree type is the **flyweight** — reused across all trees.

💡 You store **one template**, not thousands of duplicates.

---

### 🧭 TL;DR

> **Flyweight Pattern = Share common data among many similar objects.**
> “Reuse what repeats — store only what changes.”
