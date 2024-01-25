# Evan Wu - Lab 2 Report
---
## Part 1
---
ChatServer.java:
```java
import java.io.IOException;
import java.net.URI;
import java.util.*;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.

    ArrayList<String> userA = new ArrayList<>();
    ArrayList<String> stringA = new ArrayList<>();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return "hello";
        } 
        else if (url.getPath().equals("/add-message")) {
            //after split, there should be 2 items in parameters
            //idx 1 holds s <string>
            //idx 3 holds user <string>
            String[] parameters = url.getQuery().split("[=&]");
            userA.add(parameters[3]);
            stringA.add(parameters[1]);

            String resultString = "";
            String templateString = "%s: %s\n";

            for (int i = 0; i < userA.size(); i++) {
                resultString += String.format(templateString, userA.get(i), stringA.get(i));
            }

            return resultString;
        } 
        else {
            return "404 Not Found!";
        }
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
