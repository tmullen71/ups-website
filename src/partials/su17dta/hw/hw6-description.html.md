```
cacheable: false
```

## Introduction

For this assignment, you're going to do something along the lines of the prime number listing program we looked at in class, but a little bit more complicated. Namely, you're going to write a program that will take any two years (after 1582, the year the Gregorian calendar was adopted) and list all leap years between them (inclusive).

A leap year is defined as follows (From Lewis & Loftus):

>A year is a leap year if it is divisible by 4, unless it is also divisible by 100, but not 400. For example, the year 2003 is not a leap year, but 2004 is. The year 1900 is not a leap year because it is divisible by 100, but the year 2000 is a leap year because even though it is divisible by 100, it is also divisible by 400

Your program should return an error if the user attempts to input a year that is less that 1582. Also, think about how to handle the ordering of arguments (i.e, what happens if the user puts the later year first and the earlier year second). You may handle the ordering of arguments however you think is sensible, but you should make it clear that your program is checking for this possibility and handling it intelligently.

Finally, recall what I talked about in class with regard to the proper role of `main` in a program. For this assignment, please create two classes. One class should be a wrapper class that will have only a `main` method. The other class will contain the actual functionality of your program, and will not have a `main` method. In the `main` method of the first class, you'll create an instance of an object of the second class and call a method to execute its code. 

### Submission

Compress the full project directory for the completed assignment into a zip file and upload it to the [Moodle page for the assignment](https://moodle.pugetsound.edu/moodle/mod/assign/view.php?id=335271).
