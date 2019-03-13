# Objectives

This topic provides the student with knowledge and skills on:

*  **Printf() debugging concepts**

* **How to printf() debug**
  * **Pre Checks**
  * **Five steps of debugging printf()**

---

# Printf() Debugging

In this topic we're going to review the method for **Printf() Debugging**. 

**Note: Printf() is often overlooked by modern debugging tools, but is still a proven and indispensable method of debugging.** 

**To debug using printf()**
* Print variables, outputs, etc. to see if the data meets your expecations. 

**Recall `step 4: analyze snapshot`: Using printf(), we can test all of the things we think to be true** 

**Example:** A value should be 5, a return should be at this pointer, this condition should be true, As code is found that does not meet our expectations, we can begin to formulate **why** and **how**. 

---

## How to printf() Debug

Let's begin by walking through `print_demo`. 

We can do this by going through step by step. 

### Pre-Checks

**What is the program's purpose?**
  * It's a simple calculator with add, subtract, multiply and division. The program continues to run until user tells it to stop. 
**What did we expect to happen?**
**What really happened?**
* **We expected that a user would select what kind of operation they wanted to do.** 
  * **If they selected something wrong, the prompt would appear again asking for selection.** 
  * **If they selected correctly, it would then route the user to the correct function.  The function would ask for two numbers to perform some sort of math at that point. 


The value would then be returned and printed. Lastly, the program would ask if the user wants to continue. (Loop the program)
* What really happened?
  * ???
* What should of happened?
  * Same as what we expected to happen

---

### Step One: Reproduce the Bug

* Can we reproduce this issue? 

---

### Step Two: Describe the Bug

* Is it reproduceable?
* How can you make it happen again?
* What happened?
* What should of happend?
* Is it correct sometimes?
* When did it happen?
* What can support this?
* How critical is it?
* etc

---

### Step Three: Snapshot

For printf() debugging... taking a snapshot is pretty straight forward. Unlike many other methods, we aren't going to take a legit snapshot. Instead, we are going to take a logical guess. It's best to have a general idea of where the issue is happening. Otherwise, we are going to end up printing things all day. 

Let's take a look at the example:
* Where does the code first break in this program? 
* What should we print out? 
* Let's capture that data and move on.

---

### Step Four: Analyze Snapshot

As we stated above, we did not take an entire snapshot. Nor should we ever do that using printf() due to how inefficient that would be. Let's take a look at the data we did gather though:

* We have what the values actually are, did they meet our expectations? ex:
  * We have a while loop on line 22, was it's exit condition met?
  * Were the switch case conditions met?
  * Did the if statement on line 60 meet our expectations?
  * etc

The answer should be no. Something messed up. Something did not meet our expectations. What was it?

If a condition isn't being met as expected... did we set that condition up correctly? If so, why isn't the condition being met? How can we make it behave as expected?

---

### Step Five: Step 5: Fix the Bug

Now that we've identified the bug, let's fix it.

