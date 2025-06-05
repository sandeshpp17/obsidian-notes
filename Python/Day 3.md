## comments and quotes

comments can be used for 1. explaining peace of code with impacting actual one. 2. temporary making is not executable if you are still half way or the new feature is not working as expected.
use # to comment the code.
```python
print(1) # this is print but hased will not
# print(2) # this will be not printed.
```
### Strings
using string as we saw in print its takes the word that you need to print in string.

if you want to use #, use "" to print it.
```python
myStr = "To leave a message, press the # key on your phone."
print(myStr)
```
### Escape Sequences
if you want to include " in the string as "I said "WOW!" to him". then this will show error as wow is not defined. we can use \ backslash to escape the actual character.
```python
print("Backslashes \\ and single quotes \' and double quotes \" and pound signs # are awesome!")
```


# Types

When we pass the value in python then it can be classified into several types of data type.

below are basic data types.
1. string denoted as (`str`)
2. integer/numbers denoted as (`int`)
3. float/decimal-numbers denoted as (`float`)
4. boolean (`bool`) [True or False]

examples of types
```python
print(type("Hello, World"))
print(type(12))
print(type(3.14))
print(type(True))
```

```
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
```

type conversion

```python
print(type(str(12)))
print(type(int(3.14))) # for this the output will be  3

output: <class 'str'>
		<class 'int'>
```

```
# below code calculates the slice for give pizza area. we only given a length of pizza.
inputStr = 17.5
L = float(inputStr)
slice = (L*L)/100
print(int(slice))
# output = 3
```

https://cscircles.cemc.uwaterloo.ca/3-comments-literals/
https://cscircles.cemc.uwaterloo.ca/4-types/

