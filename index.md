# Week 3 Lab Report- Servers and Bugs

## Part 1
Search Engine

```
Code

```
Which methods in your code are called
What the values of the relevant arguments to those methods are, and the values of any relevant fields of the class
If those values change, how they change by the time the request is done processing

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
The expected outcome were in reverse order, not in the same order like it is supposed to be in. In the bugged filter method, if the string passes the StringChecker, then the passing string is added to index 0 of the new list. This method then filters StringChecker's condition and returns the passing strings in reversed order. 

**Connection between the symptom and bug**
The bugged filter method is returning each passing string to the front of the arrayList instead of the end the arrayList causing returned elements to be in reversed order. 
