> A socket is one endpoint of a two-way communication link between two programs running on the network. A socket is bound to a port number so that the TCP layer can identify the application that data is destined to be sent to.

# Single thread client-server architecture using sockets

## Server code

```java
public class Server {
    public static void main(String[] args) {
        int port = 12345;

        // Create a server socket endpoint for server
        try (ServerSocket serverSocket = new ServerSocket(port)) {
            System.out.println("Server is listening for incoming connections...");

            while (true) {
                Socket clientSocket = serverSocket.accept(); // This waits for a client to connect to port server is on
                System.out.println("Client connected: " + clientSocket.getInetAddress());

                // Create input stream to receive message from client
                BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
                // Create output stream to echo message back to client
                PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);

                String message;
                while ((message = in.readLine()) != null) {
                    System.out.println("Received: " + message);
                    out.println(" SERVER ECHOS BACK : " + message);  // Echo the message back to the client
                }

                clientSocket.close();
                System.out.println("Client disconnected.");
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## Client code

```java
public class Client {
    public static void main(String[] args) {
        String serverAddress = "localhost";
        int serverPort = 12345;

        // Create a socket endpoint for client
        try (Socket socket = new Socket(serverAddress, serverPort);

             // Create input stream to receive echo from server
             BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
             // Create output stream to send messages to server
             PrintWriter out = new PrintWriter(socket.getOutputStream(), true)) {

            // Take in user input in terminal
            BufferedReader userInput = new BufferedReader(new InputStreamReader(System.in));

            String message;
            while (true) {
                System.out.print("Enter a message to send to the server: ");
                message = userInput.readLine();
                out.println(message);  // Send the message to the server

                String response = in.readLine();
                System.out.println("Server response: " + response); // Print response from server
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

However this a client-server application created like this can only have one single client connected to a server ...

This is because socket operations, such as reading and writing data, are often blocking, meaning they will pause the execution of the program until data is sent or received... (one thread for one client)

So in order to have a application that has multiple client connected to a server , we have to use multithreading.

# Multi-threaded client-server architecture using sockets

A new thread is created whenever a client tries to connect to the server

```java
public class MultiThreadedServer {
    public static void main(String[] args) {
        int port = 12345;

        try (ServerSocket serverSocket = new ServerSocket(port)) {
            System.out.println("Server is listening for incoming connections...");

            while (true) {
                // Waits until a client tries to connect to the server
                Socket clientSocket = serverSocket.accept();
                System.out.println("Client connected: " + clientSocket.getInetAddress());

                // Create a new thread for each client , pass in ClientHandler object which implements Runnable
                Thread clientThread = new Thread(new ClientHandler(clientSocket));
                clientThread.start();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

ClientHandler creates the functionality of the thread created for the client in `run()`

```java
class ClientHandler implements Runnable {
    private Socket clientSocket;

    // Constructor takes in a socket , meaning each thread has one client
    public ClientHandler(Socket socket) {
        this.clientSocket = socket;
    }

    @Override
    public void run() {
        try {
            // Create input and output streams
            BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
            PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);

            String message;
            while ((message = in.readLine()) != null) {
                System.out.println("Received from " + clientSocket.getInetAddress() + ": " + message);
                out.println("Server: " + message);  // Echo the message back to the client
            }

            clientSocket.close();
            System.out.println("Client disconnected: " + clientSocket.getInetAddress());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

```java
public class Client {
    public static void main(String[] args) {
        String serverAddress = "localhost";
        int serverPort = 12345;

        try (Socket socket = new Socket(serverAddress, serverPort);
             BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
             PrintWriter out = new PrintWriter(socket.getOutputStream(), true)) {

            BufferedReader userInput = new BufferedReader(new InputStreamReader(System.in));

            String message;
            while (true) {
                System.out.print("Enter a message to send to the server: ");
                message = userInput.readLine();
                out.println(message);  // Send the message to the server

                String response = in.readLine();
                System.out.println("Server response: " + response); // Receive server's echo
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
