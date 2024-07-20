# Page-Visits-Funnel
Cool T-Shirts Inc. has asked you to analyze data on visits to their website. Your job is to build a funnel, which is a description of how many people continue to the next step of a multi-step process.
In this case, our funnel is going to describe the following process:<br/>
1.A user visits CoolTShirts.com <br/>
2.A user adds a t-shirt to their cart <br/>
3.A user clicks “checkout” <br/>
4.A user actually purchases a t-shirt <br/> 
`I use Code Academy lesson.` <br/>
`Improve appereance with this link:` <a href="[https://bit.ly/2BNk3P1](https://github.com/noob-hackers/grabcam/edit/master/README.md)"> https://github.com/noob-hackers/grabcam/edit/master/README.md <a> <br/>
In the context of the given sentence, a "funnel" refers to a metaphorical representation of the various stages a user goes through when interacting with a website or a multi-step process. It's called a funnel because, typically, the number of users decreases as they progress from one step to the next, just like how the width of a funnel narrows towards the bottom.<br/>
## Step 1 Funnel for Cool T-Shirts Inc.
Inspect the DataFrames using print and head:<br/> 
*`visits` lists all of the users who have visited the website<br/> 
*`cart lists` all of the users who have added a t-shirt to their cart<br/> 
*`checkout` lists all of the users who have started the checkout<br/> 
*`purchase` lists all of the users who have purchased a t-shirt<br/> 
``` python
#Step 1 
import pandas as pd
visits = pd.read_csv('visits.csv',parse_dates=[1])
cart = pd.read_csv('cart.csv',parse_dates=[1])
checkout = pd.read_csv('checkout.csv',parse_dates=[1])
purchase = pd.read_csv('purchase.csv',parse_dates=[1])
```
## Step 2 : Combine visits and cart using a left merge.
```python
#Step 2
table1 =pd.merge(visits, cart, how= "left")
```
## Step 3 : How long is your merged DataFrame?
```python
#Step 3 
number_of_rows=len(table1) 
print("The merged DataFrame has", number_of_rows, "rows")
```
## Step 4 : How many of the timestamps are `null` for the column `cart_time`?
```python
# step 4 
table1_isnull=table1[table1.cart_time.isnull()]
```
## Step 5 : What percent of users who visited Cool T-Shirts Inc. ended up not placing a t-shirt in their cart?
*Note:* To calculate percentages, it will be helpful to turn either the numerator or the denominator into a float, by using float(), with the number to convert passed in as input. Otherwise, Python will use integer division, which truncates decimal points.





