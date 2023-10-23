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

As a small disclaimer, I'll only be going over the methods that are shown from the code of StringServer.java. I'm aware that the code also calls method from other .java files (such as Server.start(port, new Handler()) which isn't shown, or in-built java methods).

![add-message1](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/baf1cfee-7e63-47b4-a55a-778c4ba8cd8c)
* Following the main method and going into the new Handler object, the handleRequest method is called. Then getPath() method is called as part of an if-statement. The getQuery() method is also called when the ```/add-message``` request is called.
* For the main method, the method takes in an argument for a port number that's used to start the server. It eventually calls on the handleRequest method with the ```url``` argument which is (in my case, I used port 4000) ```http://http://localhost:4000```. From there the other method takes in arguments as part of the String object methods, array methods, or array list methods.
* Since the request shown in the screenshot is the ```/add-message``` request, the only relevant values that would change is the actual string that is added to the list and a ```num``` variable that is used to keep track of the amount of strings being added.
  
![add-message2](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/90d3ccb6-02c5-4ca5-9688-30034261908b)
* Since this is the same request, the process is very similar (if not the same) as the previous screenshot. The only difference would be that it no longer has to call main and all the other methods use to start up the server (since the server is already running). The only relevant method called when this request is called is the getPath() methods for both if-statements.
* The relevant argument are the same as the previous screenshot as well except for a different string as the query. Only the content of ```stringContent``` and ```num``` changes (then again they're variables, not arguments)
* Again, same as before the only values that changes from this specific request is the ```num``` variable since it increments, and the ```stringContent``` list since it will have a different string to add to the list.


## Part 2
For this part I'll be showing a screenshot of me using the ```ls``` command to:
* Show the path to the private key
* Show the path to the public key
* Show the terminal interaction where I can login without a password

![privateKey](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/17b8d879-75b3-4d86-a5ec-fa727a8c682c)
![publicKey](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/e4155915-a5f9-412a-8c61-e51749ad05b7)
![PasswordlessLogin](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/711f0064-33e5-4eb3-95b2-082e0cd95573)

## Part 3
I definitely didn't know how to start a simple web server using Java before week 2 so all of this is very new to me. I also learned how to create my own server in Java and actually have it run and function properly. For week 3, I'm already somewhat familiar with the process of using ```ssh``` since I'm taking CSE 30 concurrently with this class so I was already exposed to the command before (albeit with GREAT difficulty).
