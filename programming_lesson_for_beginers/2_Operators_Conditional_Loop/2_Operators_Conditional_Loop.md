# Class 2. Operators, Conditional, Loop

## Review last class

### How to output

* `print("Hello, world!, name)`
* `print("Hello, world! {}".format(name))`

### Data types

### Operators

* Arithmetic `+, -, *, /, %, //, **`
* Assignment `=, +=, -=, *=, /=`
* Comparison `>, <, ==, !`
* Logical `and, or`
* Bitwise
* Membership `in, not in`
* Identity `is, it not`

## Lesson this week

### Input

```python
a = input("Input a number: ")        # type from the input is str
b = input("Input another number: ")
c = int(a) + int(b)                  # need to convert to int before calculating
d = a + b                            # if we do not use int() to convert
print("The sum is {}, not ".format(c,d))
```

### Conditional

Keywords: `if`, `elif`, `else`

#### Syntax - Age for example

```python
age = input("please input age")

if (age < 12):
    print('kid')
elif (age < 18):
    print('teenager')
else:
    print('adult')
```

#### Excercise - Odd or Even

**Check whether input number is even.**

Hint:

1. Take one input from keyboard
2. Convert it to int
3. Use if condition