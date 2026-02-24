# Java Chat Server

This is a simple chat server implemented in Java. It allows multiple clients to connect and chat with each other in real-time.

## How It Works

- The server listens for client connections on port 9090.
- Each client connects to the server and sends messages.
- Messages from any client are broadcasted to all connected clients.

## Usage

1. **Compile the Chat Server**:
   ```
   javac ChatServer.java
   ```

2. **Run the Chat Server**:
   ```
   java ChatServer
   ```

3. **Connect Clients**:
   - Use a telnet client or implement a simple Java client to connect to the server on port 9090.

## Example Java Client

To test the server, you can create a simple client:

```java
import java.io.*;
import java.net.*;

public class ChatClient {
    public static void main(String[] args) {
        try (Socket socket = new Socket("localhost", 9090)) {
            BufferedReader input = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            PrintWriter output = new PrintWriter(socket.getOutputStream(), true);

            BufferedReader console = new BufferedReader(new InputStreamReader(System.in));
            String userInput;

            while ((userInput = console.readLine()) != null) {
                output.println(userInput);
                System.out.println("Server: " + input.readLine());
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### Notes

- Ensure ports are open and firewalls are configured to allow connections.
- For a production environment, add authentication and encryption as needed.
