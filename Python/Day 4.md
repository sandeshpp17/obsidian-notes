## Input

Input function takes input from the user. when program need to take the user input then this function can be used. input only returns result in `str` we can change the type of the result using  other `datatypes`.

when no input where passed in program then we get below error.
```python
EOFError: EOF when reading a line
```

- we cannot print input() 2 time directly rather than we can store the input value in variable and manipulate it as we want.
```python
sound = input()
print(sound)
print(sound)

# below is wrong example
print(input())
print(input()) # this will cause an error.
```


## If 

`If` is the function in python which allows us to skip or execute the program on condition. if the conditions are met then the code is executed and if not then code will be skipped.

- the condition for program is True(1) then the code is executed under if statement.
- the condition for program is False(0) then the code is skipped under if statement.
- `if x < y:` means "if x is less than y"
- `if x >= y:` means "if x is greater than or equal to y"
- `if x <= y:` means "if x is less than or equal to y"

### Structure of an if statement

the structure of if statement should be in below format.
```python
if «condition»:
	# block of code
	print("This condition is true")
```
- `if` : it starts with word 'if' which indicates the funtion.
- `<conditions>` : then the condition which returns boolean value like True or False.
- `:` : ends with colon to close the statement 
- with proper indentation the block of code when condition is true.

Note:  when you use the `bool` values `True` and `False` directly in a program, they [must be capitalized or you will get an error](https://cscircles.cemc.uwaterloo.ca/console/?consolecode=print%28true%29).

#### Boolean comparisons.

if python we only compare the condition in > or < there is also way to compare its `=`(equal to ) and `!=` (not equal to). but in python we use = sign for assigning value to variable so we use == for comparison.

```python
# first code
x=int(input())
if x > 0:
   print("Positive")
if x < 0:
   print("Negative")
if x == 0:
   print("Zero")

# second code
age = int(input())
if age >= 18:
   print("You can vote")
if 0 <= age <= 17:
   print("Too young to vote")
if age < 0:
   print("You are a time traveller")
```

