# Writing to a file

```java
try (FileWriter fileWriter = new FileWriter("new.txt", true)) { // true parameter is to append content to file not overwrite
    fileWriter.write("SOME TEXT \n");
} catch (IOException ioException) {
    ioException.printStackTrace();
}
```

# Reading to a file

```java
try (FileReader fileReader = new FileReader("new.txt")) {
  //Read and print each word from file
  Scanner scanner = new Scanner(fileReader);
  while (scanner.hasNext()) {
      String word = scanner.next();
      System.out.println(word);
  }
} catch (IOException ioException) {
  ioException.printStackTrace();
}
```

Can use a buffered reader/writer instead to reduce write operations
