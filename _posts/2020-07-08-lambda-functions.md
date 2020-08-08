---
title: "Lambda Expressions: Is It Any Good ?" 
categories:
  - Python
toc: true
---

I happened to stumble upon this expression recently while going through a piece 
of code and after reading the python docs I just realised that I could very well 
survive without knowing it.  
But . . .  
There were some undoubtedly cool stuff about this expression that I liked. 
Although there exist many use cases for this, I will just go through the ones 
that I found useful and might end up using.

## What are lambda expressions ?
> Lambda expressions (sometimes called lambda forms) are used to create anonymous 
> functions.

An anonymous function refers to a function declared with no name. So while a 
normal function is created using the keyword `def`, an anonymous function is 
created using a keyword `lambda`. 

The lambda expression `lambda parameters : expression` behaves as a function 
that takes the *parameters* and returns the *expression*.

Lambda functions are syntactically restricted to a single expression. Like nested 
function definitions, lambda functions can reference variables from the containing 
scope:

## Some Use Cases
### Normal Functions
As long as the return statement can be written as a single expression any function 
can be converted to a lambda expression. For **small functions** such as the 
one shown below, I would prefer the lambda expression as it reduces the function 
to just one line and it looks a bit clean. (*just a personal preference!!*)

Both functions given below have the same call statement i.e. `time_diff(t1, t2)`.
```python
# case 1
def time_diff (t1, t2):
  return (t2 - t1)/60

# case 2
time_diff = lambda t1, t2: (t2 - t1)/60
```
### Inside Other Functions
This is a very common implementation of the lambda expression and shows it's 
true power.
```python
def power(n):
  return lambda x: x**n
square = power(2)
cube = power(3)

print(square(2))  # 4
print(cube(3))    # 27
```
### Key Functions
Key functions in Python are higher-order functions that take a parameter `key` 
as a named argument which recieves a a function. Some common key functions 
are: `sort`, `sorted`, `min` and `max`.

The following block shows the use of a key function for sorting a list of tuples. 
In this case we want to sort the list based on the first value of the tuple. 
This is done using the inbult sort function with the key recieving the name of 
the function that returns the first value.
```python
def first(pair):
  return pair[0]

pairs = [(3, 'three'), (1, 'one'), (4, 'four'), (2, 'two')]
pairs.sort(key=first)

print(pairs)  # [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]
```
The same sort could have been done using the lambda function in a much more 
concise way as shown in the example below. 
```python
pairs = [(3, 'three'), (1, 'one'), (4, 'four'), (2, 'two')]
pairs.sort(key=lambda pair: pair[0])

print(pairs)  # [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]
```

## Conclusion
There are many more applications of lambda expressions and these were just 
three cases which I found useful. 

Although lambda expressions might tempt you to write shorter codes, it does come 
with a fair share of criticism; mainly for making code hard to read for those not 
familiar with it. 

In the end choose wisely where you want to use lambda's or normal functions 
aaannd . . .

![goodtogo](/../assets/images/gtg.png)
{: style="text-align: center;"}
