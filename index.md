# Week 3 Lab Report- Servers and Bugs

## Part 1
Search Engine

```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.

    ArrayList<String> arr = new ArrayList<String>();
    ArrayList<String> str = new ArrayList<String>();
    int num = 0;
    String searched = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Items added: %d", num);
        }
        else if (url.getPath().contains("/search")) {
            String[] parameters = url.getQuery().split("s=");
            //System.out.println(arr + "!");
            for (int i = 0; i < arr.size(); i++) {
                if (arr.get(i).contains(parameters[1])) {
                    String item = arr.get(i);
                    str.add(item);
                    searched += item + " ";
                }
            }
            return String.format(searched);
        } 
        else if (url.getPath().contains("/add")) {
            String[] parameters = url.getQuery().split("s=");
            arr.add(parameters[1]);
            num += 1;
            //System.out.println(parameters[1]);
            //System.out.println(arr);
            return String.format("Added " + parameters[1] + ", Items added is " + num);
            }
            return "404 Not Found!";
    }
}

class SearchEngine {
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
`main` and `handleRequest(URI url)` are called. 

<img width="525" alt="Screen Shot 2022-10-14 at 8 47 00 PM" src="https://user-images.githubusercontent.com/114449002/195967470-84468adf-4601-4967-a976-4d0e081e0057.png">

Initially, when the server `http://localhost:4000` first starts, num is 0 and the items added to the arrayList is 0. 


<img width="578" alt="Screen Shot 2022-10-14 at 8 49 18 PM" src="https://user-images.githubusercontent.com/114449002/195967561-2d4f88a2-c04a-458b-b500-7145406d40bb.png">


As /add is used, num is incremented. For instance, when `/add?s=apple` is added to the end of `http://localhost:4000`, num would increment by one. Additionally, a message of `Added apple, Items added is 1` would appear indicating the item being added and the count of items added being 1. 


<img width="578" alt="Screen Shot 2022-10-14 at 8 50 44 PM" src="https://user-images.githubusercontent.com/114449002/195967575-895c7304-6993-41ea-ac44-afaf3cfface6.png">

When something other than /add or /search is used the website would return `404 Not Found!`

<img width="567" alt="Screen Shot 2022-10-14 at 10 52 42 PM" src="https://user-images.githubusercontent.com/114449002/195971331-9136eb47-63af-40ac-8bb1-3443015545c8.png">


When /search is utilized, it would return items previously added that contains the string after s= in `/search?s=`

## Part 2 
### Array Methods 

**testAverageWithoutLowest()**

**Failure-inducing Input**

<img width="623" alt="Screen Shot 2022-10-13 at 11 37 38 AM" src="https://user-images.githubusercontent.com/114449002/195949400-63719a83-2852-484a-baf7-2db5fa260308.png">

**Symptoms**

<img width="1148" alt="Screen Shot 2022-10-14 at 2 54 57 PM" src="https://user-images.githubusercontent.com/114449002/195949890-bae3e42a-8f38-48aa-933d-ed4a771f50b0.png">


**Bug**

Before:

<img width="290" alt="Screen Shot 2022-10-14 at 2 56 40 PM" src="https://user-images.githubusercontent.com/114449002/195950062-b076b71c-1067-4ecb-bd55-e54ad5628d1d.png">

After:

<img width="310" alt="Screen Shot 2022-10-14 at 2 57 06 PM" src="https://user-images.githubusercontent.com/114449002/195950092-7f5fe3f6-70a1-4376-b9cf-bfe538a17ffd.png">

When checking for the lowest value to add to sum, the method removes all duplicates of the lowest value rather than removing the lowest value just once. When there are duplicates of the lowest number, the method ignores all duplicates of the lowest value when it should just have just ignored the lowest value once. 

**Connection between the symptom and bug:**

When checking for the lowest value to add to sum, the method removes all duplicates of the lowest value rather than removing the lowest value just once. Therefore, when the input includes duplicates of the lowest number, the method ignores all duplicates of the lowest value when it should just have just ignored the lowest value once causing the average of inputs without lowest to differ. The average of inputs should have been 2.67 as (1 + 3 + 4) / 3 = 2.67. However, as the bugged method removes all duplicates of the lowest number, removing both 1's it becomes (3 + 4) / 3 = 2.33.

### List Methods 
**Failure-inducing Input**

<img width="1158" alt="Screen Shot 2022-10-14 at 6 26 22 PM" src="https://user-images.githubusercontent.com/114449002/195963092-026ce9bd-c3f6-4cfd-a695-a87dec763a43.png">


**Symptoms**

<img width="1158" alt="Screen Shot 2022-10-14 at 6 26 03 PM" src="https://user-images.githubusercontent.com/114449002/195963084-7837bc5e-2f7b-4c85-9844-ccbb723e50a6.png">


**Bug**

Before: 

<img width="608" alt="Screen Shot 2022-10-14 at 6 02 37 PM" src="https://user-images.githubusercontent.com/114449002/195963070-0b7371f7-fe8b-4d89-8d98-f6df8c14bc78.png">

After:

<img width="607" alt="Screen Shot 2022-10-14 at 6 03 03 PM" src="https://user-images.githubusercontent.com/114449002/195963063-25c78d63-252f-4abf-990f-dd524088f8a2.png">
The expected outcome were in reverse order, not in the same order like it is supposed to be in. 


**Connection between the symptom and bug**

The bugged filter method is returning each passing string to the front of the arrayList instead of the end the arrayList causing returned elements to be in reversed order. In the bugged filter method, if the string passes the StringChecker, then the passing string is added to index 0 of the new list. The bugged method filters strings according to StringChecker's condition and returns the passing strings in reversed order. By removing the specified place index 0 at `result.add(0, s);`, it solves the problem of returning passing strings to the front of the arrayList. 
