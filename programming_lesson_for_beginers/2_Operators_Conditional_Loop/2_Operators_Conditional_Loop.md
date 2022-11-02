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

If

```python!
age = input("please input age")

if age < 12:
    print('kid')
```

:::warning
Take a look at indenting.\
Python is a Whitespace Sensitive.
:::

if else

```python!
age = input("please input age")

if age < 12:
    print('kid')
else:
    print('not kid')
```

if, elif, else

```python!
age = input("please input age")

if age < 12:
    print('kid')
elif age < 18:
    print('teenager')
else:
    print('adult')
```

#### Excercise 1 - x,y larger?

:::info
Goal: print out `x is less than y`, `x is greater than y`, `x is equal to y`
:::

```python!
x = 7
y = 10

if x > y:
    # Add print here
elif x == y:
    # Add print here
else:
    # Add print here
```

#### Excercise 2 - Same string

:::info
Goal: print out `x string is longer than y`, 
`x str is shotter than y`, `x is greater than y`
:::

```python!
x = "hello"
y = "hello!" 

if x == y:
    print("x is identical to y")
```

:::warning
Type is important --> int and str act differently
:::

#### Excercise 4 - Odd or Even

:::info
Goal: Check input number is even or odd
:::

Hint: what is the difference between odd and even?

#### Excercise 5 - and, or

Now we combine two things together

```python!

summer = True
profession = "student"

if summer == True:
    if profession == "student": 
        print("I have summer vacation")
```

Is equivalent to 

```python!
summer = True
profession = "student"

if summer == True and profession == "student":
    print("I have summer vacation")
```