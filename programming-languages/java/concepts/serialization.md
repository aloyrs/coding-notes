# Serialization

> Serialization is the process of converting objects into a byte stream ...
> _to enable data storage, sharing, and retrieval in a compact, standardized format.._

## How to serialize an object?

```java
// Class you want to serialize should `implements Serializable`
public class User implements Serializable {
    private String name;
    private String password;

    public User(String name, String password) {
        this.name = name;
        this.password = password;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", password='" + password + '\'' +
                '}';
    }
}
```

```java
public class Main {
    public static void main(String[] args) throws IOException {

        User user = new User("aloy","aaaaa");

        // Create file to serialize to
        FileOutputStream fileOutputStream = new FileOutputStream("UserInformation.ser");

        // Create output stream to serialize to file
        ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);

        // Serialize object to a byte stream
        objectOutputStream.writeObject(user);

        // Close streams
        objectOutputStream.close();
        fileOutputStream.close();
    }
}
```

Result :

Object serialized into byte code to file `UserInformation.ser`

![Alt text](/concepts/images/serialization-result.png)

# Deserialize

> Deserialize is the process of converting a byte stream into objects (essentially reverse of serialize)

Since we stored a User object with name 'aloy' and password 'aaaaa' and serialized it into `UserInformation.ser` , now we want to deserialize it .

```java
public class Main {
    public static void main(String[] args) throws IOException, ClassNotFoundException {

        // Create file to serialize from
        FileInputStream fileInputStream = new FileInputStream("UserInformation.ser");

        // Create output stream to serialize the file input stream
        ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream);

        // Create User object to store deserialized object
        User user = (User) objectInputStream.readObject();

        // Close streams
        fileInputStream.close();
        objectInputStream.close();

        // View deserialized object
        System.out.println(user.toString());

    }
}
```

Result :

![Deserialize](/concepts/images/deserialization-result.png)

**Take Note:** Can used `transient` to mark variables in object to be not serialized

# Serial Version UID

When deserializing an object, the JVM compares the serialVersionUID of the class being loaded with the serialVersionUID that was stored with the object.

If they match, deserialization proceeds; if they don't match, a InvalidClassException is thrown, indicating a class version mismatch.

To avoid this...

**Make sure that both class structure of the serialized objects should be the same on both sides**

or

**Set a unique serial version UID for both object classes for serialization and deserialization**

```java
public class User implements Serializable {
    // A unique serial version UID for object class used in both serialization and deserialization , if match = deserialization proceeds
    private static final long serialVersionUID = 123454321;

    // Other class members and methods
}
```
