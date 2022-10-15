**Lab Report 2 CSE15l Fall 2022**

**Part 1**

This is the code for my SearchEngine class from week 2:

```
{
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

public class SearchEngine {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }
    
        int port = Integer.parseInt(args[0]);
    
        Server.start(port, new URLSplicer());
    }
}

class URLSplicer implements URLHandler{
    ArrayList<String> strings = new ArrayList<String>();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return strings.toString();
        } else if (url.getPath().equals("/search")) {
            String[] parameters = url.getQuery().split("=");
            if(parameters[0].equals("s")){
                ArrayList<String> output = new ArrayList<String>();
                for (String string : strings) {
                    if(string.contains(parameters[1])){
                        output.add(string);
                    }
                }
                return output.toString();
            }
            return String.format("N/A");
        } else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    strings.add(parameters[1]);
                    return String.format("Strings increased by %s! It's now " + strings, parameters[1]);
                }
            }
            return "404 Not Found!";
        }
    }
}
}
```

This first url localhost:4000/add?s=anewstringtoadd adds "anewstringtoadd" to the list within the class, and then displays it. handleRequest takes in the URL, and then uses if statements and methods from the URI class to parse the URL. In this case since the URL contains /add?s, the method will add "anewstringtoadd" ( spliced by the = ) to the list of strings in the class.

![Lab2-1](https://raw.githubusercontent.com/Sacha-Wallace/cse15l-lab-reports-f22/main/Lab2-1.png)

This second url localhost:4000/add?s=pineapple adds "pineapple" to the class's list, and prints it. As before, handleRequest takes in the URL and splices it with if statements. This works the same as the URL above this one.

![Lab2-2](https://raw.githubusercontent.com/Sacha-Wallace/cse15l-lab-reports-f22/main/Lab2-2.png)

The third url localhost:4000/search?s=app queries the list to find strings containing "app". handleRequest takes in the URL and parses it uses the URI methods. If it contains "search?s" then it will iterate through the list creating a new array containing elements matching the parameter.

![Lab2-3](https://raw.githubusercontent.com/Sacha-Wallace/cse15l-lab-reports-f22/main/Lab2-3.png)


**Part 2**

**Bug One**

In ArrayExamples.java, the method reverseInPlace() had an issue with how it accomplished its goal.

Below is an example of a test run on this method in which the input induced a failure.

![ArrayTests](https://raw.githubusercontent.com/Sacha-Wallace/cse15l-lab-reports-f22/main/ArrayTests.png)

The method is supposed to take in an array and then return it in reverse order -- however with an input of {"1", "2", "3"}, the method output {"3", "2", "3"} as shown below. 

![ArrayTestsFailedOutput](https://raw.githubusercontent.com/Sacha-Wallace/cse15l-lab-reports-f22/main/ArrayTestsFailedOutput.png)

This is the code behind the method:

![ArrayTestsBugCode](https://raw.githubusercontent.com/Sacha-Wallace/cse15l-lab-reports-f22/main/ArrayTestsBugCode.png)

As the function iterates through the array, it replaces the current iterative with its mirror on the opposite side of the array. However, the issue with that is for example you will set the last entry equal to the first entry. Logically this sounds correct, as you want to reverse it, but the issue is that the first entry has already been modified to match the last entry. This is why our output is {"3", "2", "3"}, as the index 2 was set to equal the new value of index 0, rather than its original. 

**Bug Two**

In ListExamples.java, the method testFilter() had an issue with the order in which its elements were added to the list. 

Below is an example of a test run on this method in which the input induced a failure

![ListTestsTest](https://raw.githubusercontent.com/Sacha-Wallace/cse15l-lab-reports-f22/main/ListTestsTest.png)

The method is supposed to return a new list with the elements in the same order, removing those who don't comply with the StringChecker's rule. In this case, the checker would only remove if the string was longer than 2 characters. The method takes in an input of {"1", "2", "3"}, but outputs {"3", "2", "1"}.

![ListTestsFilterFailedOutput](https://raw.githubusercontent.com/Sacha-Wallace/cse15l-lab-reports-f22/main/ListTestsFilterFailedOutput.png)

This is the code behind the method:

![ListTestsBugCode](https://raw.githubusercontent.com/Sacha-Wallace/cse15l-lab-reports-f22/main/ListTestsBugCode.png)

As the for loop iterates through the original list, adding the string elements to the new list, it adds them at index 0. Doing this in order through a list will reverse it, which explains why the input of {"1", "2", "3"} outputs {"3", "2", "1"}. In order to fix this all that was needed to be done was add an index counter, and increment it each string.


