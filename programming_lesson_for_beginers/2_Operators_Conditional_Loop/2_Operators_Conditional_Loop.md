# Operators, Conditional, Loop

## Review last class

### How to output

* `print("Hello, world!, name)`
* `print("Hello, world! {}".format(name))

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
a = input("Input a number: ")
b = input("Input another number: ")
c = int(a) + int(b)
print("The sum is {}".format(c))
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