# sp24-lab9
Materials for week 9 lab in CS-370, which includes Ch. 16 "Object Persistence" adapted from [Software Design by Example](https://third-bit.com/sdxpy/) by Greg Wilson.

_March 26, 2024_

Organization:
* SDX-ch16: The code files for the _SDX Ch. 16_ activity (as downloaded directly from the book website, unmodified) 

## Team Members for Part 1
Enter your names here

## Team Roles for Part 1
Who will start out as
* DRIVER: Terence
* NAVIGATOR: Coden

You will switch halfway through this activity.

## Part 1 Documentation

Write your answers to the questions below.

* What were the main ideas from SDX chapter 16?
- Building a version control from scratch and accounting for different data types. 
* What questions did you have about the material in the chapters? What did you find confusing?
- We found the section of Alliasing to be confusing. 

### Exercise 0: Running the tests

Run the tests in all three test modules. (I've added some code to make this feasible.) Verify that all tests pass.

### Exercise 1: Testing objects.py

There is a glaring omission in the given code:a
There is no test module for `objects.py`! 

Copy `test_builtins.py` to a new file named `test_objects.py`. 
Then modify it to test `objects.py` instead ofa` builtins.py`. 
(Make sure you add the new file to your git repositiory.)

I thought of two strategies. Implement whichever you prefer:

1. Adapt each of the given tests to use the object-oriented interface presented by `objects.py`. 
2. Add convenience methods save and load to `objects.py`. 

After doing this exercise, explain the strategy you chose, and why.

### Exercise 2: Refactoring `SaveObjects.save`

In `objects.py`. find the implementation of the save method.
Refactor for understandability by renaming a variable and introducing an explaining variable. 
Run the corresponding test module to verify that your refactorings didn't break anything.

After doing this exercise, briefly explain what you changed.

We didn't add an explaining variable, but we renamed the variables that were there to be more self-explanatory (like changing 'method' to 'methodname' since it's not actually a method).

### Exercise 3: Understanding code

Answer the following questions:

1.  When we create an alias marker, why is there a colon at the end of the line 

        alias:12345678:

    (Hint: Look at the implementation of `LoadObjects.load`.) 

    -Fields only splits on one colon, which would be the first one. LoadObjects can't handle aliasing, it would be an unknown object type because the key 'alias' doesn't have an associated method.

2.  Why doesn’t `LoadAlias.load` calculate object IDs? 
    Why does it use the IDs saved in the archive instead?

    -LoadAlias.load has fields that split on 2 colons, cutting the input into key, ident, and value. The load function checks to see if they key is "alias", checks to see if we've already seen it, then loads the value from it. Since it's loading, we just need to know what's saved, we only need to check if the alias already exists. If there isn't anything saved with that ID, then we can't load anything.

### Exercise 4: Strings

Modify the framework so that strings are stored using escape characters
like `\n` instead of being split across several lines.

I suggest doing this in `objects.py`. 
Use test-driven development:
Start by changing the tests in `test_objects.py` to use the new string format. 
The tests should now fail.  You will know you have correctly implemented this change when the tests pass again.

### Exercise 5: Versioning

We now have several versions of our data storage format. 
Early versions of our code can’t read the archives created by later ones, 
and later ones can’t read the archives created early on 
(which used two fields per line rather than three). 
This problem comes up all the time in long-lived libraries and applications, 
and the usual solution is to include some sort of version marker 
at the start of each archive to indicate what version of the software 
created it (and therefore how it should be read). 
Modify the code we have written so far to do this.

