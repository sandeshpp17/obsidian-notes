
<<<<<<< HEAD
### Strings

All data stored on a computer in the sequence of 0 and 1.
Number are stored internally in a 0-1 binary format.
we use the string to store alphabetical and numerical data which later stored in binary format.
#### Manipulating strings as sequences of characters

each string word has its index. TO manipulate a string we need to be able to access the individual characters that make up a string.

```python
S[index]
```
```python
Index: 0  1  2  3  4  5  6  7  8  9 10 11 12
Char.: H  e  l  l  o  ,     W  o  r  l  d  !
```

**len** : 
len is used to find the length of string that we can use to printing the last word in string.

=======
### String Manipulation.

in python we often use strings to manipulate the string we can use `len` function.
i can print the length of a particular string. by using same `len` function we can get a specific word from string.

**String cutting**
>>>>>>> origin/main
```python
myString = 'Weighty'
print(myString[1:6])
print('magic'[3:3])
print('chump'[0:4])
```
<<<<<<< HEAD

**cutting string** :  first index start with 0 and last index is len(x)-1 we can cut the string using index number.
```python
myString = 'Weighty'
print(myString[1:6])
print('magic'[3:3])
print('chump'[0:4])
```

**Pasting strings**: `+`

We all know that 1+2=3. With strings, instead we get the following result:

=======
it can work like above. To get the number of characters in a string
`len(S)` gives you the total number of characters in the string, since it starts with index `0`, the last character is at index `len(S)-1`.

**String addition**
It can be use the add two strings.
>>>>>>> origin/main
```python
result = 'one' + 'two'
print(result)
print(len(result))
<<<<<<< HEAD

# below is for multiplication
print("hots" * 2)
print("mi"+("s"*2+"i")*2+"ppi")
```

**Character codes**: `ord`, `chr`

all modern computers have a standard set of characters for the numbers between 32 and 255. Here is a list of the characters with numbers between 32 and 127:


> [!NOTE] Character code
> ord: 32  33  34  35  36  37  38  39  40  41  42  43  44  45  46  47
chr:      !   "   #   $   %   &   '   (   )   *   +   ,   -   .   /
ord: 48  49  50  51  52  53  54  55  56  57  58  59  60  61  62  63
chr:  0   1   2   3   4   5   6   7   8   9   :   ;   <   =   >   ?
ord: 64  65  66  67  68  69  70  71  72  73  74  75  76  77  78  79
chr:  @   A   B   C   D   E   F   G   H   I   J   K   L   M   N   O
ord: 80  81  82  83  84  85  86  87  88  89  90  91  92  93  94  95
chr:  P   Q   R   S   T   U   V   W   X   Y   Z   [   \   ]   ^   _
ord: 96  97  98  99  100 101 102 103 104 105 106 107 108 109 110 111
chr:  `   a   b   c   d   e   f   g   h   i   j   k   l   m   n   o
ord: 112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 127
chr:  p   q   r   s   t   u   v   w   x   y   z   {   |   }   ~

Exercise:

print next character of given alphabet but print A for Z 
```python
x = input()
if x == "Z":
   print(chr(ord("A")))
else:
   print(chr(ord(x)+1))
```


## Math

### Math Operators
- **power** : `a ** b` its use for power function. e.g.: 2^3
- **integer division**: operator `a // b` computes the "quotient" of `a` divided by `b` and ignores the remainder. For example, `14 // 3` produces `4`.
- **modulus**: operator `a % b` computes the remainder when `a` is divided by `b`. For example, `14 % 3` produces `2`.

```
Egg cartons each hold exactly 12 eggs. Write a program which reads an integer number of eggs from `input()`, then prints out two numbers: how many cartons can be filled by these eggs, and how many eggs will be left over. For example, the output corresponding to `27` eggs is
```
```python
cart = input()

print(int(cart) // 12)
print(int(cart) % 12)
```

```python
# divisible & not divisible
a = int(input())
b = int(input())

if a % b == 0:
   print("divisible")
else:
   print("not divisible")
```

=======
```


> [!NOTE] String addition to int
> If you want to concatenate numbers, you need to convert them to str first. Otherwise you will get one of two errors, depending on the order you tried. Run this program to see the errors that can occur.

**Character codes: `ord`, `chr`**

```python
print(ord('a'), ord('b'), ord('A'), ord('B'), ord(' '))
print(chr(35), chr(43), chr(100))
```

### Math Operators
>>>>>>> origin/main
