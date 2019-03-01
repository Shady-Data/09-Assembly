# Reading and Understanding Errors

There are multiple types of errors in the C Programming langauge. An **error** is simply an illegal operation that was performed by the user. This operation results in some sort of abnormality of the program. The most common types of errors are:

* **Syntax Error**
* **Run-Time Error**
* **Linker Error**
* **Logical Error**
* **Semantic Error**

---

## Syntax Errors

These occur when you violate the rules of the C Programming syntax; aka your code is just not written following the rules of C. This is a very common reason for no compilation. Some examples of this are:

* Missing curly-bracket or parenthesis
* Missing semi-colon
* Failing to declare a variable before using it
* Mis-spelling a function or variable

Example of compile output:

`error: expected ';' before '}' token`

### Identifying Syntax Errors

These errors can be identified easily. First off, the program never compiles. That is a large indication of a Syntax error. GCC and IDEs with built in debuggers will also produce information that indicate an `error`. 

### Finding Syntax Errors

Luckily for us, these errors are often easy to find. Rather you compiled via terminal or IDE... you will generally recieve the error, the problem and the line number on which it happened. Below is an exmaple of us missing a semi-colon and the GCC output of such a mistake. 

```
yes_senpai@pop-os:~/CLionProjects/debugging_test$ gcc main.c 
main.c: In function ‘main’:
main.c:4:30: error: expected ‘;’ before ‘return’
     printf("Hello, World!\n")
                              ^
                              ;
     return 0;
```

As we can see here, the mistake is on line 4 character 30 in main.c (main.c:4:30):

`main.c:4:30: error: expected ‘;’ before ‘return’`

### Fixing Syntax Errors

Syntax errors are often easy to fix. Identify and find the errors location in code. Then simply fix the syntax. Re-compile. 

---

## Run-Time Errors

These errors occur during run-time (program execution) and are after successful compilation. These types of errors are not easy to find... there are no messages pointing to the location from the compiler. One example is the division by zero error. 

```
warning: division by zero [-Wdiv-by-zero]
    div = n/0;
```

### Identifying Run-Time Errors

Run-time errors may be a bit more difficult to find than Syntax Errors. But luckily for us, most compilers will produce a `warning` indicating where the problem is. 

### Finding Run-Time Errors

As said above, compilers will often produce a `warning` when there is a run-time error. This warning should contain a line and character at which the problem happened. For instance, if you divided by zero:

```
main.c: In function ‘main’:
main.c:4:14: warning: division by zero [-Wdiv-by-zero]
     int x = 4/0;
```

We can see that the error happened on line 4:14 inside of main.c. 

### Fixing Run-Time Errors

Run-Time errors are pretty easy to fix. We need to first identify the warning, if needed look it up, and apply a fix. Often times run-time errors may require us to change a bit more code than just one character or line. Say it was `4/n` rather than `4/0`. If a loop had asigned `n` the value of 0... then we need to fix the condition of the loop or the statement itself. 

---

## Linker Errors

These errors occur because some function or library that is needed could not be found. This occurs during the *linking stage* and will generally prevent an executable from being generated. We will go over the linking stage more in a later section. One common example of this is misspelling a name of a function when you declare, define or call it. 

`file.o(address): undefined reference to 'Foo(void')`

### Identifying Linker Errors

Linker errors are very easy to identify. In this case, the `warning implicit declaration of function 'foo'` should give us all of the information we need. 

```
Scanning dependencies of target debugging_test
[ 50%] Building C object CMakeFiles/debugging_test.dir/main.c.o
/home/yes_senpai/CLionProjects/debugging_test/main.c: In function ‘main’:
/home/yes_senpai/CLionProjects/debugging_test/main.c:8:5: warning: implicit declaration of function ‘foo’; did you mean ‘Foo’? [-Wimplicit-function-declaration]
     foo();
     ^~~
     Foo
[100%] Linking C executable debugging_test
[100%] Built target debugging_test

Build finished
```
`no output on executable`

### Finding Linker Errors

If you reference the compiler warning above, the line and character number is provided above. This warning points to the `foo()` call in main. `foo()` was declared as `Foo()` above main (or in a header) with a capital H. 

### Fixing Linker Errors

In this case, all the programmer has to do is fix the name. But this is generally all that has to be done in all cases. 

---


## Logical Errors

This one may not even seem like an error at first. The program compiles and executes... sometimes no warnings are even given. But this error becomes apparent when incorrect output is given. These are very common errors done by green programmers. Mixing up `==` with `=` or forgetting a semicolon are common examples. 

### Identifying Logical Errors

This type of error can be very hard for a programmer to identify. Errors are often not given, compilers often do not say anything, the program often compiles and there is virtually no indication other than output that you were not expecting. 

The easiest way to identify this type of error is by setting up unit tests ahead of time and following principles of TDD. Otherwise, you will have to begin taking snapshots and debugging until you find the root cause/causes. 

### Finding Logical Errors

If a unit test was created, the unit test will fail. That will your red flag. If no unit test was created, then you must take a snapshot and begin analyzing the information until you find an abnormality. Finally, you will have to begin stepping back into your code until you find the root cause or causes. 

### Fixing Logical Errors

Once the code is identified, the programmer will generally have to change up the logic. Maybe you asigned a variable rather than using the equal-to operator. Maybe the condition needs a `>=` rather than just a `==`. Maybe you are itterating the wrong direction. Etc. Fixing the error is as simple as fixing the logic. This will be a common occurance for a newer programmer. 

---

## Semantic Errors

These errors occur because the statements within the program are not meaningful to the compiler. The syntax used is correct... but maybe the programmer used the wrong variables, operations or order. For example, initializing a variable and trying to increment it without declaring the variable. Or doing something like `a + b = c`. 

### Identifying/Finding Semantic Errors

Semantic errors will be very similar to Logical Errors. You often won't even know you have a bug until you see the output. Again, unit testing should make this error more easy to identify. Otherwise, you will have to find the abnormality and determine what the error is once you find it. Viewing variable values are a very useful way to identify this error. 

### Fixing Semantic Errors

Just like fixing logical errors, the programmer will have to fix their error in code by adjusting the order, operations or variables used. 

---

# Some Common Examples

### Core Dump (Segmentation Fault)

Core Dumps are a type of Run-Time error. They occur when you access memory that does not belong to you. For instance, when a piece of code tries to do read/write operations in a read only location of memory. Or if there is memory corruption. 

#### Some Examples of this are:

```c
char x[5] = "Yall";
x[6] = 'l';
```
This will cause a `SIGARBT` which will dump the core. In this example, it's practically gurenteed to happen every single time. Here is the complete error:

```
*** stack smashing detected ***: <unknown> terminated

Process finished with exit code 134 (interrupted by signal 6: SIGABRT)
```

But something like this may not even throw a segfault.... until it does. 

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {
    char *buf = malloc(10);
    memset(buf, 'a', 10);
    printf("%s\n", buf);

    free(buf);

    memset(buf, 'b', 10);
    printf("%s\n", buf);
    return 0;
}
```

**If this didn't throw a segfault, why not?**

Well, even though we ran `free()`... that doesn't mean the OS took care of that action right away or even marked that it did (if in fact it did already free that memory). So it may not even know you are accessing freed memory... until it does. This "bug" may not even be noticeable at first. All may be working well. Until 1500 lines later... then it decides to throw a segfault. 

### Forgetting to Declare Variables

In C, every var must be declared for it's type. Many programers may forget to declare a variable. Especially if one is creating a for loop. 

### More Common Errors:

* [Common Errors 1](http://www.edm2.com/0504/12cerr.html)
* [Common Errors 2](https://www.thecrazyprogrammer.com/2014/08/15-common-errors-in-c-and-cpp-programming.html)
* [Common Compiler Errors](http://aop.cs.cornell.edu/errors/index.html)
* [Top 20 C Pointer Errors/Mistakes - How to Fix Them](https://www.acodersjourney.com/top-20-c-pointer-mistakes/)

