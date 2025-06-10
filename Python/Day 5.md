## Debug
Programmer write a program sometime he make a mistake in value or logic and later on it causes the error or unnatural behavior of program. To find-out which line of code is causing this kind of behavior we have to debug the code. 

The longer that you do programming, the better you will become at avoiding and fixing mistakes, but here we'll try to give you some very general and useful advice. We'll explain the following techniques:

- build one part at a time
- solve some examples by hand
- plan your code before you start writing it
- write the code
- test the examples that you have solved by hand
- test additional examples including “borderline” and random cases

For example of donut which is called timbit. 
so are give some pack of value and we have to calculate overall cost for number of timbits

| Number          | Price |
| --------------- | ----- |
| 1               | $0.20 |
| 10(small box)   | $1.99 |
| 20 (medium box) | $3.39 |
| 40 (large box)  | $6.19 |

> [!NOTE]
> **Algorithm to calculate the price of any number of timbits**
> 
> 1. get the input number of timbits
> 2. keep track of the total cost, starting from zero
> 3. buy as many large boxes as you can
>     1. calculate the number of timbits still needed
>     2. update the total price
> 4. buy a medium box if you can and repeat steps A. and B.
> 5. buy a small box if you can and repeat steps A. and B.
> 6. buy individual timbits and repeat step B.
> 7. output the total cost
> 

```python
timbitsLeft = int(input()) # step 1: get the input
totalCost = 0              # step 2: initialize the total cost

# step 3: buy as many large boxes as you can
bigBoxes = int(timbitsLeft / 40)
totalCost = totalCost + bigBoxes * 6.19    # update the total price
timbitsLeft = timbitsLeft - 40 * bigBoxes  # calculate timbits still needed

if timbitsLeft >= 20:                # step 4, can we buy a medium box?
    totalCost = totalCost + 3.39
    timbitsLeft = timbitsLeft - 20
if timbitsLeft >= 10:                # step 5, can we buy a small box?
    totalCost = totalCost + 1.99
    timbitsLeft = timbitsLeft - 20   # change 20 with 10 because we should be reducing with pack

totalCost = totalCost + timbitsLeft * 20 # step 6 replace 20 with 0.20 because 1 timit vaule
print(totalCost)                         # step 7

```

carefully observe the step no. 5 and 6 
For step 5:
	if timbits are above 10 then totalcost should be update with addition of $1.99 and it should get reduced. but we have 11 timbets and it reduces by 20 then we will get -9 so if we are considering for 10 then we should be reducing by 10 
For step 6:
where we are given the totalcost adds with remaining timbits and multiplied by 20. but if get 3 timbit then total cost should gets upto $60 which is wrong because 1timbit = 0.20 

https://cscircles.cemc.uwaterloo.ca/6d-design/