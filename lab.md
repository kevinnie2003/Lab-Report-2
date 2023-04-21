# Lab Report 2 By Kevin Nie
# Part 1
Code for StringServer: (Server.java is implemented and also shown below)

StringServer.java
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    ArrayList<String> str = new ArrayList<String>();
    String toReturn;
    public String handleRequest(URI url) {
        toReturn = "";
        if (url.getPath().contains("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                str.add(parameters[1]);
                for (int i = 0; i < str.size(); i++){
                    toReturn += (str.get(i) + "\n");
                }
                return toReturn;
            }
        }
        return "404 Not Found!";
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if (args.length == 0) {
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }
        int port = Integer.parseInt(args[0]);
        Server.start(port, new Handler());
    }
}
```
Server.java
```
// A simple web server using Java's built-in HttpServer

// Examples from https://dzone.com/articles/simple-http-server-in-java were useful references

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url);
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;
    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }
    public void handle(final HttpExchange exchange) throws IOException {
        // form return body after being handled by program
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            // form the return string and write it on the browser
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class Server {
    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started! Visit http://localhost:" + port + " to visit.");
    }
}
```

Screenshots of using /add-message:

<img width="418" alt="截屏2023-04-20 18 49 30" src="https://user-images.githubusercontent.com/122497019/233521713-013f5680-bc51-4ffe-b166-d735a066c11b.png">

For the first screenshot with the link "http://localhost:4000/add-message?s=happy":

1. The main method in StringServer.java is called with the argument 4000 as the port number.
2. The start method in Server.java is called with the arguments 4000 (port) and a new Handler object (handler).
3. The handleRequest method in Handler class is called with the URL "http://localhost:4000/add-message?s=happy".

Relevant arguments and values of fields:

* The port number is 4000.
* The Handler object has an ArrayList<String> field named str which is empty initially.
* The URI object passed to the handleRequest method has the path "/add-message" and the query "s=happy".
    
Changes in values of fields:

* The str ArrayList in the Handler object will add the string "happy" to the list, making its content: ["happy"].

<img width="397" alt="截屏2023-04-20 18 50 08" src="https://user-images.githubusercontent.com/122497019/233521772-87cb1e44-6b25-4bb2-8106-c993daaf1af2.png">

For the second screenshot with the link "http://localhost:4000/add-message?s=sad":

1. The handleRequest method in Handler class is called with the URL "http://localhost:4000/add-message?s=sad".

Relevant arguments and values of fields:

* The port number is still 4000.
* The Handler object has an ArrayList<String> field named str which now contains ["happy"].
* The URI object passed to the handleRequest method has the path "/add-message" and the query "s=sad".

Changes in values of fields:

* The str ArrayList in the Handler object will change again as a result of this request. It will add the string "sad" to the list, making its content: ["happy", "sad"].










# Part 2
Here is one example from Lab 3 that has a bug, and I will show how I tested it and the systom, as well as the fixed code.


1. A failure inducing input for the buggy program as a test:
    
```
  import static org.junit.Assert.*;
  import org.junit.*;

  public class ArrayTests {
    @Test
    public void testReversed2() {
        int[] input1 = { 1, 2, 3, 4 };
        assertArrayEquals(new int[] { 4, 3, 2, 1 }, ArrayExamples.reversed(input1));
    }
  }
```

2. An input that doesn’t induce a failure, as a test:

```
  import static org.junit.Assert.*;
  import org.junit.*;

  public class ArrayTests {
    @Test
    public void testReversed1() {
    int[] input1 = {};
    assertArrayEquals(new int[] {}, ArrayExamples.reversed(input1));
    }
  }
```

3. The symptom, as the output:

<img width="926" alt="截屏2023-04-19 17 24 37" src="https://user-images.githubusercontent.com/122497019/233502796-1a96f092-209c-411b-b423-f251aa59274d.png">

The bug is that arr value should be passed to newArray, but the code did the opposite way so the empty newArray is passed to newArray. It should return the newArray instead of the original array “arr” as well.

4. The original code with the bug:
    
```
  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
                                  
```
                                  
The fixed code:
                                  
```
  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for (int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```

Change the code so that the reversed array of input array is stored in newArray and return the newArray.



# Part 3
One thing that I learned from labs that is very important and beneficial is that how to use Github and write a markdown file. Now I can use Github to explore thousands of projects I am interested in, as well as writing my own projects. I can also easily create a page of my own by writing a .md file one Github.
