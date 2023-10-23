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
To give credit where it is due, I used the NumberServer.java file provided from the [wavelet github page](https://github.com/ucsd-cse15l-f23/wavelet) as a base to create the StringServer.java file. I only edited a few lines of code to make it function as a StringServer specified for the lab report (but much if not most of it is from NumberServer.java).  

To show that the ```/add-message``` request works, I will provide two screenshots using the request.  
And for each screenshots I will also describe:
* The methods that are called in the code
* The relevant argument to those methods and the values of relevant fields of the class
* How the values change from this specific request

As a small disclaimer, I'll only be going over the methods that are shown from the code of StringServer.java. I'm aware that the code also calls method from other .java files (such as Server.start(port, new Handler()) which isn't shown).

![add-message1](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/baf1cfee-7e63-47b4-a55a-778c4ba8cd8c)


