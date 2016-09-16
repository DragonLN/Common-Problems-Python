#5 Common Problems Faced by Python Beginners

Are you in the process of learning Python? It’s a fantastic language to learn, but as with any language, it does present challenges that can seem overwhelming at times, especially if you’re teaching yourself.

Given all the different ways of doing things in Python, we decided to compile a helpful list of issues that beginners often face — along with their solutions.

<img src="https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2016/05/1462964485python-logo.jpg" >

----
##1. Reading from the Terminal

If you’re running a program on the terminal and you need user input, you may need to get it through the terminal itself. (Other alternatives include reading a file to get inputs.)

In Python, the `raw_input` function facilitates this. The only argument the function takes is the prompt. Let’s look at a small program to see the result:
```Python
name = raw_input('Type your name and press enter: ')
print 'Hi ' + name
```

If you save those lines in a file (with a `.py` extension) and execute it, you get the following result:

    Type your name and press enter: Shaumik
    Hi Shaumik

One important thing to note here is that the variable is a string, and you need to filter and convert it to use it in a different form (like an input for the number of iterations or the length of a matrix):

```Python
name = raw_input('Type your name and press enter: ')
print 'Hi ' + name
num = raw_input('How many times do you want to print your name: ')
for i in range(int(num)):
    print name
```

----
##2. Enumerating in Python

Python often presents ways of doing things different from other popular programming languages like C++ and Java. When you traverse an array in other languages, you increment an integer from `0` and access the corresponding elements of the array. The following shows a crude way of doing the same:

```Python
for (int i = 0; i < array_length; ++i)
    cout << array[i];
```

However, in Python, you can simply traverse each element of the array without using the indices at all:

```Python
for item in array:
    print item
```

What if there’s a need to access the indices too? The `enumerate` function helps you do so. Enumeration of an array (or a "list", as it’s known in Python) creates pairs of the items in an array and their indices. The same can be demonstrated as follows:
```Python
>>> x = [10, 11, 12, 13, 14]
>>> for item in enumerate(x):
...     print item
...
(0, 10)
(1, 11)
(2, 12)
(3, 13)
(4, 14)
```

Imagine a situation where you need to print every alternate item in an array. One way of doing so is as follows:
```Python
>>> for index, item in enumerate(x):
...     if index % 2 == 0:
...         print item
...
10
12
14
```

----
##3. Executing an External Command through Python

At some point, you may need to execute a terminal command within a Python script. This can be achieved through the `call` function under the `subprocess` module. There are many ways to do this, one of which is shown below:

```Python
>>> from subprocess import call
>>> call('cal')
     March 2016
Su Mo Tu We Th Fr Sa
       1  2  3  4  5
 6  7  8  9 10 11 12
13 14 15 16 17 18 19
20 21 22 23 24 25 26
27 28 29 30 31

0
```

The last zero in the output shows that the subprocess we created within our script ended normally. In other words, there were no issues in running the command.

If you need to use arguments for the command, you need to append them to the main command as a list. For instance, to run the command `ls -l`, the following needs to be done:

```Python
>>> from subprocess import call
>>> call(['ls', '-l'])
total 16
-rw-------@ 1 donny  staff  439 Oct 21 16:06 chess.csv
-rw-r--r--  1 donny  staff   72 Mar  1 17:28 read.py
0
```

To check what happens to the `0` when something wrong happens, we can run a git command in a non git repository:

```Python
>>> from subprocess import call
>>> call(['git', 'status'])
fatal: Not a git repository (or any of the parent directories): .git
128
```

In the output, the second line is the output of the command, whereas `128` is the exit code.

----
##4. Working with Exceptions
Python is an interpreted language, which means that the code is executed line by line. If an error is encountered on a line, further execution of the code stops. However, you can handle known exceptions in Python using the try-except block. Let’s look at a simple example, by generating a runtime error of dividing by `0`:

```Python
>>> x = 1/0
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: integer division or modulo by zero
```

When the interpreter reaches this line, your program execution stops completely! However, using the try-except block can help avoiding the same.
```Python
>>> try:
...     x = 1/0
... except:
...     print "Some error occurred"
...
Some error occurred
```

When such an error occurs within the `try` block, the interpreter just executes the `except` block. The `except` block can further be extended by catching individual errors:

```Python
>>> try:
...     x = 1/0
... except ZeroDivisionError:
...     print "You tried to divide by zero"
... except:
...     print "Some unknown error occurred"
...
You tried to divide by zero
```

You can go one step ahead, catch the exception and further process it (like log the error somewhere) by modifying the `except` block:
```Python
>>> try:
...     x = 1/0
... except Exception as e:
...     print "Exception occurred: " + str(e)
...
Exception occurred: integer division or modulo by zero
```


----
##5. Working with Modules

While looking at the code of others, you’ll often encounter this block of code:

```Python
def some_function():
    ...

if __name__ == '__main__':
    ...
```
This is used frequently when you create modules in Python. Ideally, the code in the last block usually demonstrates some basic usage of the function(s) above. When you run the file in the terminal, this code is executed. However, if you use this module in a different file for the purpose of using the function, this block is not executed. Confusing? Let’s understand this better through an example:
```Python
# File print.py
def print_me():
    print "me"

# demonstrating use of print_me
print_me()
```

Now, if I import this file to use the function in a new file, watch what happens:
```Python
>>> import print
me
>>>
```

The function gets executed as soon as you import the file. To avoid this, we put the function under a `if __name__ == '__main__':` block:
```Python
# File print.py
def print_me():
    print "me"

if __name__ == '__main__':
    # demonstrating use of print_me
    print_me()
```

When we modify the code, the `print_me()` function is executed only when you run it as a file, but not when you import it as a module:
```Python
>>> import print
>>>
```

----
##Final Thoughts

If Python isn’t your first programming language, it’s going to take some time to adjust to its way of doing things. I recommend you watch an interesting YouTube video of Raymond Hettinger explaining this Pythonic Way of programming. In this post, I’ve attempted to cover a few of these Pythonic issues.

How was your Pythonic journey, or how is it still going? Do you prefer doing these tasks differently? Do let us know in the comments below!


----
##Refer
[SitePoint](https://www.sitepoint.com/5-common-problems-faced-by-python-beginners/)
