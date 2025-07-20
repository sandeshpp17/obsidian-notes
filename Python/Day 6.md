
### String Manipulation.

in python we often use strings to manipulate the string we can use `len` function.
i can print the length of a particular string. by using same `len` function we can get a specific word from string.

**String cutting**
```python
myString = 'Weighty'
print(myString[1:6])
print('magic'[3:3])
print('chump'[0:4])
```
it can work like above. To get the number of characters in a string
`len(S)` gives you the total number of characters in the string, since it starts with index `0`, the last character is at index `len(S)-1`.

**String addition**
It can be use the add two strings.
```python
result = 'one' + 'two'
print(result)
print(len(result))
```


> [!NOTE] String addition to int
> If you want to concatenate numbers, you need to convert them to str first. Otherwise you will get one of two errors, depending on the order you tried. Run this program to see the errors that can occur.

**Character codes: `ord`, `chr`**

```python
print(ord('a'), ord('b'), ord('A'), ord('B'), ord(' '))
print(chr(35), chr(43), chr(100))
```

### Math Operators
