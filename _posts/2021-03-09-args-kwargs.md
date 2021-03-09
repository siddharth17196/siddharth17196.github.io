---
title: "Unpacking Operators"
categories:
  - Python
toc: true
---

Ever come across a time when you wanted to extract all elements of a list using 
a single expression. Well, in that case unpacking operators are exactly what you needed.
The two operators used are the (*) for iterable objects and (**) for dictionaries. 

## * Operator

Unpacking is allowed inside sets, lists and tuples.
```python
>>> print(*[1, 2, 3])
1 2 3
>>> print(*(1, 2, 3))
1 2 3
>>> [*range(4), 4]
[0, 1, 2, 3, 4]
>>> {*range(4), 4}
{0, 1, 2, 3, 4}
```

It can also be used to unpack or merge multiple iterables 
```python
>>> list1 = [1, 2, 3]
>>> list2 = [4, 5, 6]
>>> print(*list1, *list2)
1 2 3 4 5 6
>>> merged_lst =[*list1, *list2]
>>> print(merged_lst)
[1, 2, 3, 4, 5, 6]
```

The (*) operator can also be used for variable assignments. In the example below, 
the first element gets assigned to **'a'**, the last element gets assigned to **'c'** 
and the rest of the elements are assigned to **'b'** in the form of a list.

If there are only 2 elements in the list in that case they would be assigned to 
**'a'** and **'c'** respectively while **'b'** would be an empty list.
```python
>>> list1 = [1, 2, 3, 4, 5]
>>> a, *b, c = list1
>>> print(f"a:{a}, b:{b}, c:{c}")
a:1, b:[2, 3, 4, 5], c:6
```

### * Operator on strings
The operation on strings is also somewhat similar to that of list.
```python
>>> text = "random"
>>> *a, b = text
>>> print(f"a:{a}, b:{b}")
a:['r', 'a', 'n', 'd', 'o'], b:'m'
>>> *a, = text
>>> a
['r', 'a', 'n', 'd', 'o', 'm']
```

## \*\* Operator

The '**' operator is used to unpack dictionaries. This can also be used to 
merge/append dictionaries.

*Note:* Using just one asterisk on dictionaries would only return its keys.

```python
>>> d = {'a':1, 'b':2, 'c':3}
>>> print(*d)
a b c
>>> print({**d, "d":4})
{'a': 1, 'b': 2, 'c': 3, 'd': 4}
```

## \*args and \*\*kwargs
Often many python functions have their arguments as *args and **kwargs. It was only 
after quite some time that I came to know what that meant.

*args and **kwargs allows one to pass multiple arguments or keyword arguments to 
functions. Let us consider a function that returns the sum of 2 
integers.
```python
def getsum(a, b):
    return a + b

getsum(2, 3) #5
```
However, this function is limited to only 2 integers. Here's where the **\*args** 
variable comes to play. This lets us send any number of arguments to the function.
```python
def getsum(*args):
    s = 0
    for number in args:
        s += number
    return s

getsum(1, 2, 3, 4)  #10
```
The important part here is the asterisk: the unpacking operator that was explained 
in the above section. The iterable object that we get on passing this to the 
function is a **tuple**. The variable name **args** is just a way of representing and 
could be changed to any other name.


**\**kwargs** is similar to that of args but instead of taking positional arguments, 
it takes named arguments.
```python
def getname(**kwargs):
    return kwargs['firstname'] + " " + kwargs['lastname']

getname(firstname="James", lastname="Bond")     #James Bond
```
In the following example, a function takes a fixed set of arguments and a 
unpacked dictionary is passed in the function call. However, it is important here 
that the keys of the dictionary have the same name as the function arguments.
```python
def getsum(a, b):
    return a+b

d = {'a':1, 'b':2}
getsum(**d)     #3
```


### Ordering of Arguments in function

In python the order of arguments in functions are paramount (else would result 
in syntax error). Just as non-default arguments precede default arguments, in this 
positional arguments precede keyword (named) arguments.
```python
def sample_func(a, b, *args, **kwargs):
    ...
    pass
```
