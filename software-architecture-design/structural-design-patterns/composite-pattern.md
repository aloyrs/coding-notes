# 📁 Composite Pattern – File System Example

### 🧠 Concept

The **Composite Pattern** lets you **treat individual objects (files)** and **compositions of objects (folders)**
in a **uniform way**, forming a **tree structure**.

> 💡 Think of it like your computer’s file explorer — you can “open,” “delete,” or “rename” both files _and_ folders the same way.

---

### 🧱 Key Roles

| Role                   | Description                                                 |
| ---------------------- | ----------------------------------------------------------- |
| **Component**          | Common interface for both files and folders.                |
| **Leaf (File)**        | Represents indivisible objects — no children.               |
| **Composite (Folder)** | Represents containers that can hold files or other folders. |
| **Client**             | Works with all components through the same interface.       |

---

### 💻 Java Example – File System

```java
// ----- Component -----
interface FileSystemComponent {
    void showDetails(String indent);
}

// ----- Leaf -----
class FileItem implements FileSystemComponent {
    private String name;

    public FileItem(String name) {
        this.name = name;
    }

    @Override
    public void showDetails(String indent) {
        System.out.println(indent + "📄 File: " + name);
    }
}

// ----- Composite -----
class Folder implements FileSystemComponent {
    private String name;
    private List<FileSystemComponent> children = new ArrayList<>();

    public Folder(String name) {
        this.name = name;
    }

    public void add(FileSystemComponent component) {
        children.add(component);
    }

    public void remove(FileSystemComponent component) {
        children.remove(component);
    }

    @Override
    public void showDetails(String indent) {
        System.out.println(indent + "📁 Folder: " + name);
        for (FileSystemComponent child : children) {
            child.showDetails(indent + "   ");
        }
    }
}

// ----- Client -----
public class Main {
    public static void main(String[] args) {
        // Create individual files
        FileSystemComponent file1 = new FileItem("resume.pdf");
        FileSystemComponent file2 = new FileItem("photo.jpg");
        FileSystemComponent file3 = new FileItem("notes.txt");

        // Create folders
        Folder docsFolder = new Folder("Documents");
        Folder picsFolder = new Folder("Pictures");
        Folder rootFolder = new Folder("Home");

        // Compose the structure
        docsFolder.add(file1);
        picsFolder.add(file2);
        rootFolder.add(docsFolder);
        rootFolder.add(picsFolder);
        rootFolder.add(file3);

        // Display full structure
        rootFolder.showDetails("");
    }
}
```

**Output:**

```
📁 Folder: Home
   📁 Folder: Documents
      📄 File: resume.pdf
   📁 Folder: Pictures
      📄 File: photo.jpg
   📄 File: notes.txt
```

---

### 🧠 Flow Summary

| Step | Action                              | Result                                            |
| ---- | ----------------------------------- | ------------------------------------------------- |
| 1️⃣   | Create `FileItem` objects           | Represent leaf nodes (no children)                |
| 2️⃣   | Create `Folder` objects             | Composite nodes that can contain other components |
| 3️⃣   | Add files/folders into folders      | Build a tree hierarchy                            |
| 4️⃣   | Call `showDetails()` on root folder | Recursively traverses and displays structure      |

> 🧩 Both **files** and **folders** share the same interface (`FileSystemComponent`),
> so the client can treat them uniformly.

---

### 🪜 Summary

- Builds **part–whole tree structures** (folders inside folders).
- Treats **leaf and composite objects** the same.
- Makes recursion and traversal simple — each component handles its own behavior.
- Promotes **open/closed principle** — easily add new component types (like shortcuts).

---

### 🧾 Real-world Analogy

💻 **Operating System File Explorer**

- **File** → Cannot contain anything (Leaf)
- **Folder** → Can contain files and folders (Composite)
- Both can be opened, renamed, or deleted using the same commands.

💡 The system doesn’t care if it’s dealing with a file or folder — same interface!

---

### 🧭 TL;DR

> **Composite Pattern = Treat individual and group objects uniformly in a tree structure.**
> “Folders contain files and other folders — and both can be handled the same way.”
