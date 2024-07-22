# Page-Visits-Funnel
Cool T-Shirts Inc. has asked you to analyze data on visits to their website. Your job is to build a funnel, which is a description of how many people continue to the next step of a multi-step process.
In this case, our funnel is going to describe the following process:<br/>
1.A user visits CoolTShirts.com <br/>
2.A user adds a t-shirt to their cart <br/>
3.A user clicks “checkout” <br/>
4.A user actually purchases a t-shirt <br/> 
<img title="Page-Visits-Funnel" src="https://imgurl.ir/uploads/j44525_Page-Visits-Funnel.png">
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
```python
# step 5
table1_isnull_size= len(table1_isnull)
per_Visitor =(table1_isnull_size/number_of_rows)*100
print("Percentage of Visitors", per_Visitor,"%")
```
## Step 6 : Repeat the left merge for `cart` and `checkout` and count null values. What percentage of users put items in their cart, but did not proceed to checkout?
```python
#step 6
table2=pd.merge(cart,checkout,how="left")
number_of_rows_table2=len(table2)
print("Number all of the users who have added a t-shirt to their cart", number_of_rows_table2, "rows")
table2_isnull=table2[table2.checkout_time.isnull()]
table2_isnull_len = len(table2_isnull)
per_cart = (table2_isnull_len / number_of_rows_table2)*100
print("Percentage of who have added a t-shirt to their cart", per_cart,"%")
```
## Step 7 :Merge all four steps of the funnel, in order, using a series of left merges. Save the results to the variable `all_data`.
Examine the result using `print` and `head`.
```python
#Step 7
all_data=visits.merge(cart,how="left").merge(checkout,how="left").merge(purchase,how="left")
print("Merge table of all data ",all_data.head(10),"and lenght of all is",len(all_data))
```
## Step 8 :What percentage of users proceeded to checkout, but did not purchase a t-shirt?
```python
#Step 8
table3=pd.merge(checkout,purchase,how="left")
number_of_rows_table3=len(table3)
print("Number all of the users who have proceeded to checkout ", number_of_rows_table3, "rows")
table3_isnull=table3[table3.purchase_time.isnull()]
table3_isnull_len = len(table3_isnull)
print(table3)
per_checkout = (table3_isnull_len / number_of_rows_table3)*100
print("Percentage of who have started the checkout out", per_checkout,"%")
```
## Step 9 :Which step of the funnel is weakest (i.e., has the highest percentage of users not completing it)?
How might Cool T-Shirts Inc. change their website to fix this problem?
```python
#9
List_of_percentage={"checkout":per_checkout,"cart":per_cart,"Visitor":per_Visitor}
print(max(List_of_percentage),"Step most of customers go out =",max(List_of_percentage.values()))
```
# Average Time to Purchase
We need to calculate times of purches. 
## Step 10: Using the giant merged DataFrame all_data that you created, let’s calculate the average time from initial visit to final purchase. 
Add a column that is the difference between purchase_time and visit_time.
```python
#10
all_data['time_to_purchase'] = \
    all_data.purchase_time - \
    all_data.visit_time
```
## Step 11: Examine the results by printing the new column to the screen.
```python
#11
print(all_data.time_to_purchase)
```
## Step 12: Calculate the average time to purchase by applying the .mean() function to your new column.
```python
#12
print(all_data.time_to_purchase.mean())
```
--- 
# Full Code
```python
import codecademylib3
#Step 1 
import pandas as pd
visits = pd.read_csv('visits.csv',parse_dates=[1])
cart = pd.read_csv('cart.csv',parse_dates=[1])
checkout = pd.read_csv('checkout.csv',parse_dates=[1])
purchase = pd.read_csv('purchase.csv',parse_dates=[1])
#Step 2
table1 =pd.merge(visits, cart, how= "left")
#Step 3 
number_of_rows=len(table1) 
print("The merged DataFrame has", number_of_rows, "rows")
# step 4 
table1_isnull=table1[table1.cart_time.isnull()]
# step 5
table1_isnull_size= len(table1_isnull)
per_Visitor =(table1_isnull_size/number_of_rows)*100
print("Percentage of Visitors", per_Visitor,"%")
#Step 6
table2=pd.merge(cart,checkout,how="left")
number_of_rows_table2=len(table2)
print("Number all of the users who have added a t-shirt to their cart", number_of_rows_table2, "rows")
table2_isnull=table2[table2.checkout_time.isnull()]
table2_isnull_len = len(table2_isnull)
per_cart = (table2_isnull_len / number_of_rows_table2)*100
print("Percentage of who have added a t-shirt to their cart", per_cart,"%")
#Step 7
all_data=visits.merge(cart,how="left").merge(checkout,how="left").merge(purchase,how="left")
print("Merge table of all data ",all_data.head(10),"and lenght of all is",len(all_data))
#Step 8
table3=pd.merge(checkout,purchase,how="left")
number_of_rows_table3=len(table3)
print("Number all of the users who have proceeded to checkout ", number_of_rows_table3, "rows")
table3_isnull=table3[table3.purchase_time.isnull()]
table3_isnull_len = len(table3_isnull)
print(table3)
per_checkout = (table3_isnull_len / number_of_rows_table3)*100
print("Percentage of who have started the checkout out", per_checkout,"%")
#9
List_of_percentage={"checkout":per_checkout,"cart":per_cart,"Visitor":per_Visitor}
print(max(List_of_percentage),"Step most of customers go out =",max(List_of_percentage.values()))
#10
all_data['time_to_purchase'] = \
    all_data.purchase_time - \
    all_data.visit_time
#11
print(all_data.time_to_purchase)
#12
print(all_data.time_to_purchase.mean())
```





