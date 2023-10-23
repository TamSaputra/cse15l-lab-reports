# Lab Report 2 (Week 3)
## Part 1
For Part 1, I made a new server called ```StringServer.java``` that takes in a string and list them in order as you add more string.  
The code for ```StringServer.java``` is displayed below:  
```
//Code taken from NumberServer.java of Week 2 Lab. Edited to work as specified for lab report 2.

import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {

    ArrayList<String> stringContent = new ArrayList<String>();
    int num = 0;

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            if(num > 0){
                String stringList = "";
                for(int i = 0; i < num; i++){
                    String stringToAdd = stringContent.get(i);
                    stringList += String.format("%d. %s\n", i + 1, stringToAdd);
                }
                return stringList;
            }
            else{
                return String.format("The list is currently empty. Use \"/add-message?s=<string>\" to add more strings to the list.");
            }
        } else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    stringContent.add(parameters[1]);  
                    num += 1;
                    String stringList = "";
                    for(int i = 0; i < num; i++){
                         String stringToAdd = stringContent.get(i);
                    stringList += String.format("%d. %s\n", i + 1, stringToAdd);
                    }
                    return stringList;
                }
            }
            return "404 Not Found!";
        }
    }
}

class StringServer {
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

