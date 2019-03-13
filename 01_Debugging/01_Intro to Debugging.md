# Intro to Debugging

![](/assets/debugging.jpg)

## What is debugging?

By now, you have more than likely experienced C code that would not compile. You probably asked yourself, 

* **Why did this happen?** 
* **What can I do to fix this?**

Or maybe you asked yourself,

* **Why isn't my code passing this test case?**
* **My code compiled, what do these warnings mean though?**
    * **Why is my program doing something I didn't expect?**

Debugging is using a tool that doesn't necessarily give us the answer... but helps us find it. **De** means to denote removal. **Bug** is just an error, flaw, failure or fault within a program. This can be in the compilation process or some incorrect code. 

## Tools Used

Many different tools exist. One must keep in mind their development enviroment when choosing debugging tools. For our case, we our in Linux (Debian base) programming in C. That leaves us with a ton of different tools we can utilize. For the sake of this course, our tools are listed below:

* GDB
* `<stdio>`
* CLion
* VS Code
* Terminal Output
* IDA Pro

## Debugging Process

There are two general questions to ask yourself when you run into a bug:

* **What did you expect your code to do?**
* **What happaned instead?**

Once you have those questions answered, there are five general steps to take when debugging:

1. Reproduce the bug
   1. If it's a compilation issue... try compiling again... and maybe one more time. If you are recieving the same compile error and the code still doesn't compile, then it's time to look at **why**. 
   2. If the code compiles but the program crashes, repeat the above and observe what is happening. Can you reproduce this bug?
   3. If the code compiles and everything works fine, but you notice it's not what you expected to happen. Can you reproduce this?
2. Describe the bug
3. Capture a snapshot of your program when the bug happens. Take note of all the variable's values, location of code (if applicable), states of the program, etc. 
4. Analyse the snapshot. Based on the details, try to determine the cause of the bug. This can be done in a number of ways. But generally it falls to the process of confirming the many things you believe are true, until you find something that's not. 
5. Fix the bug, be sure to check new bugs don't occur after fixing. 

Sounds kind of simple... right? Well, this has the potential to be a daunting task. This is where TDD really comes into play; to prevent as many bugs as possible during development. There are many tools, as listed above, that make this entire process easier. We will be going over a multitude of ways to identify, confirm, capture, anaylse and fix said bug. 

---


### Step One: Reproduce the Bug

Being able to reproduce the bug is extremely important. This helps identify if it's even a bug at all. This also gives us crucial data for the remaining steps. 

* **What happened?**
* **What did you expect to happen?**
* **When did it happen?**
* **How did you manage to reproduce it?**

Here's the first step. You just attempted to compile your code. You expected at least one major thing to happen... 

#### Did your code compile?

If no, then that is a bug. Something in your code is causing a compilation error. Run it again to be sure that it's not your IDE causing the error or some "glitch". If it still fails, mark it down as a compilation bug. You managed to **reproduce** it, just by re-compiling the code. Move on to step 2. 

If yes, then you are solid. Continue.

#### Did the program compile, yet crashes on launch or at some point when it's not expected to crash?

If yes, then something in your code has been done wrong. **Can you reproduce this?** Yes? **How did you reproduce this?** Mark it down as a critical bug, move on to step 2. 

If no, then continue. 

#### Did the program do as you expected? Or did your test case pass?

If no, then something in your code has been done wrong or you programmed your test case incorrectly. **Can you reproduce this output?**. If yes, then **how did you reproduce it?** Does it sometimes return the correct expectation? Mark it down as a bug, move on to step 2. 

If yes, then either your code is fine. 

---

### Step 2: Describe the Bug

Step 2 is deeply involved within step one. The questions we asked will describe the bug for us. Of course, not all questions apply below. 

* **Is it reproduceable?**
* **How can you make it happen again?**
* **What happened?**
* **What should of happend?**
* **Is it correct sometimes?**
* **When did it happen?**
* **What can support this?**
* **How critical is it?**
* **etc**

The above is often times called a **bug report.**

---

### Step 3: Snapshot

Taking a snapshot of the program requires us to essentially gather all information about the program in it's state where the bug is present. The closer to the bug appearing, the better. Things such as: 

* **variable values**
* **stack information**
* **resources**
* **error/warning messages**
* **test assertions**
* **compile errors**
* **IDE break on exceptions**
* **etc**

We gather this information by using tools such as debuggers, I/O, test assertions, etc. 

---

### Step 4: Analyze Snapshot

`Confirm the things you believe to be true... until you find something that's not true`

During this step, we are going to analyze all of the information we have gathered above. We are going to confirm conditions, variables, stack allignment, etc. Whenever we find something in code that is producing an output that we did not expect... we need to attempt to figure out why that is happening. This often requires us to backstep starting at the first thing we find to be false... until we run into a series of things we find to be true. Generally this location in code will often contain the bug. Though sometimes... it can be more complicated than that.

We will of course go over many different methods of analyzing and identifying bugs during this chapter. 

---

### Step 5: Fix the Bug

This part is pretty straight forward. Once we have identified what caused the bug... we need to fix said code. But there's a little more to it than that. We also need to ensure no further bugs were created by squashing that bug. This can be done by simply running the code again or creating an identical snapshot and re-analyzing the same "ladder" we just analyzed. We will discuss this step a tad more later in the chapter. 
