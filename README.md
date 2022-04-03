# Amazon Retail analysis 
Here I am going to analyze the amazon dataset and at the end give my views on it.

## Description
In this code, I have done a visual, tabular, and quantitative analysis of the retail monthly sales of amazon for the fiscal year 2019 in python. I can use the output to strategize marketing, distribution, and production of electronic goods according to location type and revenue generated for the year 2019. I have clean the data, performed analysis, and created bar charts and line graphs to draw conclusions.

## Getting started 
### Dependencies
Here are some software dependencies for my project:
- Python
- Anaconda 
- Pandas 
- Numpy
- Seaborn
- Matplotlib

### Prerequisites
- Learn basics of python 
- Learn basic functiuons of libraries like pandas,matplotlib,seaborn etc.

### Installing
- Python(3.9) :- https://www.python.org/downloads/release/python-390/
- Anaconda :- https://www.anaconda.com/
- Pandas :- https://pandas.pydata.org/docs/getting_started/install.html
- numpy :- https://numpy.org/install/
- seaborn :- https://seaborn.pydata.org/installing.html
- matplotlib :- https://matplotlib.org/stable/users/installing/index.html


### Executing program
1. **Load required libraries** as below:<br>
   <p>import numpy as np <br>
   import pandas as pd <br>
   import seaborn as sns <br>
   import matplotlib.pyplot as plt <br>
   %matplotlib inline<br></p>
   
2. **Load the the file and append all files**:<br>
    <p>import os<br>
    file_path = []<br>
    for dirname, _, filenames in os.walk('archive'):<br>
        &nbsp&nbsp&nbsp&nbsp for filename in filenames:<br>
            &nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp file_path.append(os.path.join(dirname, filename))<br>
    df = pd.DataFrame()<br>
    for file in file_path:<br>
    &nbsp&nbsp&nbsp&nbsp temp = pd.read_csv(file)<br>
    &nbsp&nbsp&nbsp&nbsp df = pd.concat([df, temp], axis = 0, ignore_index = True)</p>
3. **For Data cleaning remove missing values**:<br>
      <p>df = df.dropna(how='all', inplace=False)<br>
      df.drop(df.loc[df['Order ID'] =='Order ID'].index.tolist(), axis=0,inplace=True)<br>
      df.info()<br>
      df<br></p>
4. **Data pre processing**:<br>
      <p>df['Quantity Ordered'] = pd.to_numeric(df['Quantity Ordered']).astype(int)<br>
      df['Price Each'] = pd.to_numeric(df['Price Each']).astype(float)<br>
      df['Order Date'] = pd.to_datetime(df['Order Date'])<br>
      df['Revenue'] = df['Quantity Ordered'] * df['Price Each']<br>
      df['Month'] = df['Order Date'].dt.month<br>
      df['Hour'] = df['Order Date'].dt.hour<br>
      #Using lambda to take out the middle part of Purchase Address, store in new column as City<br>
      df['City'] = df['Purchase Address'].apply(lambda x: x.split(',')[1])<br>
      df.head()<br></p>
5. **Getting Insights from data**:<br>
      <p>monthly_revenue = df.groupby('Month').sum()<br>
      monthly_revenue<br>
      year_revenue = monthly_revenue['Revenue'].sum()<br>
      year_revenue<br></p>
6. **Visual representation of monthly revenue in 2019**:<br>
      <p>plt.figure(figsize = (24, 6))<br>
      sns.barplot(x = monthly_revenue.index, y = monthly_revenue['Revenue'], data = monthly_revenue, palette = 'muted')<br>
      plt.title('Monthly Revenue in 2019', fontname = 'cursive', weight = 'bold')<br>
      # x-label<br>
      plt.xlabel('Months', weight = 'bold')<br>
      # y-label<br>
      plt.ylabel('Revenue(USD)', weight = 'bold');<br></p>
7. **Cities and their sales**:<br>
      <p>plt.figure(figsize = (24, 6))<br>
      sns.barplot(x = city_sales.index, y = city_sales['Revenue'], data = city_sales, palette = 'muted')<br>
      plt.title('Sales in each cities', fontname = 'cursive', weight = 'bold')<br>
      #x-label<br>
      plt.xlabel('City', weight = 'bold')<br>
      #y-label<br>
      plt.ylabel('Sales(USD)', weight = 'bold');<br></p>
8. **Peak hours of the day**:
      <p>plt.figure(figsize=(24, 4))<br>
      plt.plot(hourly_sales.index, hourly_sales['Quantity Ordered'])<br>
      plt.grid(True)<br>
      plt.title('Hourly Sales', fontname='cursive', weight='bold')<br>
      #x-label<br>
      plt.xlabel('Hour')<br>
      #y-label<br>
      plt.ylabel('Number of Orders');<br></p>
      
9. **Products Sold**
      <p>plt.figure(figsize = (24, 6))<br>
      sns.barplot(x = products.index, y = products['Quantity Ordered'], data = products, palette = 'muted')<br>
      plt.title('Products sold in numbers', fontname = 'cursive', weight = 'bold')<br>
      #x-label<br>
      plt.xlabel('Product', weight = 'bold')<br>
      degrees = 60<br>
      plt.xticks(rotation = degrees)<br>
      #y-label<br>
      plt.ylabel('Quantity', weight = 'bold');<br></p>

### Insights drawn from Analysis
- Decembeer month witnessed highest sales(4613443.34) and subseqently january month had the lowest sales(1822256.73).
- Austin city needed maximum attention as there was a lowest revenue there, whereas San francisco has the highest revenue.
- Number of products sold in each city helped amazon to decide the reorder quantity and the stock to be maintained.
- Moreover, By analyzing peak hours, company can hire people accordingly and utilize human and other resources better.

### Help
- Make sure to install all dependencies.
- Nevigate your files properly in the notebook file.

### Author
Name :- **Harsh Bhatt**

### Version History
- 0.1
  - Initial Release

### License
This project is licensed under the [Harsh Bhatt] License

### Acknowledgments
- Learning basic Python = <a href="https://www.w3schools.com">W3Schools</a><br>
- understand slaes analysis  = <a href="https://www.kaggle.com/code/zhonghanzhou/sales-analysis">Kaggle</a><br>
- Solving errors  = <a href="https://www.w3schools.com">Stackoverflow</a>
- - - -
