# Restaurant-Ratings-Data-Analysis-Project
This project presents a detailed exploratory data analysis (EDA) of a restaurant dataset using Python. The goal is to uncover meaningful insights into customer ratings, city-wise restaurant distribution, popular cuisines, and service features such as online delivery and table booking.  Using libraries like pandas, NumPy, matplotlib, and seaborn.
cleaned, explored, and visualized to answer key analytical questions, such a

This project analyzes a restaurant dataset to uncover insights into customer ratings, location patterns, popular cuisines, and more. Using Python libraries like pandas, matplotlib, and seaborn, the data was cleaned, explored, and visualized to answer key analytical questions, such as:

Which cities have the most listed restaurants?

What are the top-rated restaurants and cuisines?

Does online delivery affect customer ratings?

What types of restaurants generally receive higher ratings?


## Technologies Used
Python
Pandas
NumPy
Matplotlib
Seaborn
Jupyter Notebook
## Project Highlights:
# import libries
```python
import pandas as pd
import numpy as np 
import matplotlib.pyplot as plt #visualizing data
%matplotlib inline
import seaborn as sns
```

 # import data set
```python
import pandas
dataframe = pandas.read_csv('blinkit_data.csv')
dataframe
```

# check top 10 records
```python
dataframe.head(10)
```

# check tail 10 records
```python
dataframe.tail(10)
```


#  shape,info columns,datatype of columns

```python
print("the size of data is : " ,dataframe.shape)
dataframe.columns
dataframe.dtypes
```
# data cleaning
```python
print(dataframe['Item Fat Content'].unique())  #3 unique value present in Item Fat Content in thi columns
dataframe['Item Fat Content']=dataframe['Item Fat Content'].replace({'low fat':'Low Fat',
                                                                     'LF':'Low Fat',
                                                                     'reg':'Regular'})
print(dataframe['Item Fat Content'].unique())

```
 
 # Bussines Requirments
 # KPI Requirment
```python
# total sales
Total_sales=dataframe ['Sales'].sum()

# average sales
Avg_sales=dataframe ['Sales'].mean()

# how many items sold
no_of_item_sold=dataframe ['Sales'].count()

# average rating
Avg_rating=dataframe['Rating'].mean()

# display
print(f"Total_sales :${Total_sales:,.0f}")

print(f"Avg_sales :${Avg_sales:,.0f}")

print(f"no_of_item_sold :${no_of_item_sold:,.0f}")
print(f"Avg_rating  :${Avg_rating:,.0f}")
```


# # Charts Requirment
  # total sales by Fat Content
```python
sales_by_fat =dataframe.groupby('Item Fat Content')['Sales'].sum()
plt.pie(sales_by_fat,labels= sales_by_fat.index,
        autopct='%.1f%%',
        startangle= 90)

plt.title('sales_by_fat')
plt.axis('equal')
plt.show()
```
 # Total sales by Item type
```python
sales_by_type = dataframe.groupby('Item Type')['Sales'].sum().sort_values(ascending=False)  # Fixed 'Flase' to 'False'

plt.figure(figsize=(10, 6))
bars = plt.bar(sales_by_type.index, sales_by_type.values)
plt.xticks(rotation=90)  # Fixed 'rotation ==90' to 'rotation=90'
plt.xlabel('Item Type')
plt.ylabel('Total_sales')
plt.title('Total Sales By Item Type')

for bar in bars:
    # Fixed syntax errors in the text placement
    plt.text(
        bar.get_x() + bar.get_width()/2,  # Fixed missing comma
        bar.get_height(),
        f'{bar.get_height():,.0f}',  # Fixed 'bar,get_height' to 'bar.get_height' and added comma for formatting
        ha='center', va='bottom',  # Fixed string literal issue with quotes
        fontsize=8
    )
plt.tight_layout()
plt.show()
```

 # Total Sales by Outlet Establishment
```python
sales_by_year = dataframe.groupby('Outlet Establishment Year')['Sales'].sum().sort_index()

plt.figure(figsize=(9, 5))
plt.plot(sales_by_year.index, sales_by_year.values, marker='o', linestyle='-')

plt.xlabel('Outlet Establishment Year')
plt.ylabel('Total Sales')
plt.title('Outlet Establishment')

# Add data labels to each point
for x, y in zip(sales_by_year.index, sales_by_year.values):
    plt.text(x, y, f'{y:.0f}', ha='center', va='bottom', fontsize=8)

plt.tight_layout()
plt.show()
```

 # Total Sales by Outlet  
```python
sales_by_size = dataframe.groupby('Outlet Size')['Sales'].sum()

plt.figure(figsize=(4, 4))
plt.pie(sales_by_size, labels=sales_by_size.index, autopct='%1.1f%%', startangle=90)
plt.title('Outlet Size')
plt.tight_layout()
plt.show()
```

 # Sales by Outlet Location
 ```python
sales_by_location = dataframe.groupby('Outlet Location Type')['Sales'].sum().reset_index()  # Fixed typo: rset_index -> reset_index
sales_by_location = sales_by_location.sort_values('Sales', ascending=False)

plt.figure(figsize=(8,3))
ax=sns.barplot(x='Sales',y='Outlet Location Type', data=sales_by_location)
plt.title('Total Sales by Outlet Location Type')
plt.xlabel('Total Sales')
plt.ylabel('Outlet Location Type')

plt.tight_layout()
plt.show()

```
# findings
**Total Sales** amounted to $1,201,681, with 8,523 items sold and an average sales value of $141.

The **average customer rating** across products is 4.0, indicating high overall satisfaction.

**Low Fat** items generated the highest sales among fat content categories, highlighting consumer preference for healthier options.

Snack Foods, Dairy, and Fruits & Vegetables were the top-selling item types.

**Outlets established** in 1985 and 1999 showed strong and consistent sales over the years.

Small-sized outlets generated the majority of revenue, suggesting that smaller formats can still achieve high sales efficiency.

Locations classified as Tier 1 (Urban) had the **highest total sales**, followed by Tier 2 cities, reflecting urban market dominance.

Outlet Size and Location Type play a significant role in sales performance.

Data cleaning was necessary to standardize fat content categories, improving accuracy in grouped analysis.


 

# conclusion 
This project delivers meaningful insights into restaurant performance by analyzing sales and ratings data from various perspectives, including item types, fat content, outlet size, and location.
Key perormance indicators show that:
The business achieved total sales of $1,201,681 through 8,523 items sold, with an average rating of 4.0, reflecting strong customer satisfaction.
Low Fat items generated a majority of the sales, indicating health-conscious customer preferences.
Among all item types, a few categories such as Snack Foods and Fruits & Vegetables contributed significantly to revenue.
Outlets established in earlier years (e.g., 1985, 1999) still perform strongly, showing sustained business presence.
Small-sized outlets surprisingly contribute a large portion of sales, showing that size doesn’t always limit performance.
Sales are highest in Tier 1 and Tier 2 cities, where urban demand and accessibility support strong performance.
Overall, the analysis suggests that maintaining product diversity, focusing on popular item types, and strategically expanding in high-performing locations can further improve business outcomes. The combination of high sales, strong ratings, and clear customer preferences offers valuable direction for future growth and decision-making
 
- 
