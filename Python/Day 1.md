Third party site :https://cscircles.cemc.uwaterloo.ca/
tutorial: https://docs.python.org/3/tutorial/
https://www.python.org/about/gettingstarted/


## printing Hello world

```python
print("Hello, world!")
```

- print is python command 
- () contains the word that you want to print.
- word or message that you want to print must in " ".

## Variables
- variable is the storage for the data in a program which stores the value.
- if you assign the new value of old variable it will be over written.
```python
x = 10
y = 15
x = y -x
print(x)

output: x = 5
```

- pseudocode is using the providing temporary variable to preform task.
```python
# you want to exchange the value of x and y then use other variable

temp = x  # x is 10 then x is stored in temp 
x = y   # y = 20 now y is x so y value is assigned to x now x is 20
y = temp # so temp is 10 which x previously so y value is 10
```



Summary: 
end link: https://cscircles.cemc.uwaterloo.ca/1-variables/

learned able print which is used to print the message using print command with ("message") in it.
variable is used to store the data in program. 

## Errors

in the program you will encounter lots of error preventing to run the application. there are different types of error or bug that needs to be fixed to run the application.

1. syntax error
	this error is like you have forget the put () or " " in the program.
	in English the sentences are written in grammatical way if the grammar is not proper then it make no sense what you are trying to say. same in python if the program is wrongly written then python is unable to understand is and show error.
```python
print "hello, world" # this is much like syntax error.
``` 

2. runtime error
	when the variable is not defined you will get the runtime error.
```python
print (gretting) # runtime error for this program as gretting is not define
```

3. logic error
	when the program run without any error but i will not provide the output as expected then logic error is in the program.

4. special word
	don't use the word like `False, None, True, and, as, assert, break, class, continue, def, del, elif, else, except, finally, for, from, global, if, import, in, is, lambda, nonlocal, not, or, pass, raise, return, try, while, with, yield` this are the function predefined in the python.


syntax error
```python
print(1+2+3+4+5+) # here the addition plus is added due to that syntax error.
```

- if the word has not put in "" then is considers as variable
```python
print("Hello")
username = sandesh # here sandesh is variable if we put "" then its string
print(username)
```

logic error
- You are going shopping for meat and milk, but there is tax. You buy $2.00 of milk and $4.00 of meat, and the tax rate is 3%. Print out the total cost of your groceries (you don't need to print the dollar sign).
```python
meatPrice = 4.00
meatTax = 0.03 * meatPrice
milkPrice = 2.00
milkTax = 0.03 * milkPrice
print(meatTax + meatPrice + milkTax + meatPrice)
```

in above example check the addition at last line there 2 time meatprice it should be meatprice and milkprice

 