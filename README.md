# Datacamp Pandas Curriculum

# pandas_practice

practicing pandas based on datacamp videos with various datasets

## 1. Transforming DataFrames

**DataFrame: homelessness**
*Index(['region', 'state', 'individuals', 'family_members', 'state_pop'], dtype='object')*

- [x] Introduction
  - Pandas is built on NumPy and Matplotlib to store and visualize data and is used to handle DataFrames.

***
Quickly explore data using the *.head()* method

- **This returns the first 5 rows and all columns associated with a dataframe**

***
To get a sense of each column and the datatype each contains, use the *.info()* method

- **This returns a table that contains the number of columns, the number of non-null values, and the datatype. Memory usage is also available**

***
Statistical summaries can be obtained using the *.describe()* method

- **This will include count, mean, stdev, min, and quartiles of each column of the dataframe**

***
Common Attributes:

- shape: rows and column sizes
- columns: names of columns
- index: number of rows
- values: each value in a NumPy Array

***

- [x] Inspecting DataFrames
  - Using .head(), .info(), .shape, and .describe() to get a feel for the DataFrame, homelessness
- [x] Parts of DataFrames
  - Using .values, .columns, and .index to get the attributes of the DataFrame, homelessness

***

- [x] Sorting and Subsetting
  - Sorting can be done on a specific column or set of columns

***
Sort by a single column by applying the *.sort_values()* method with the column of interest as the argument in the method:

        df.sort_values("*arg*")
***
Multiple columns can be sorted via a list as an argument of the columns of interest in the sort_values() method:

        df.sort_values(["*arg[0]","arg[1]*"])
***
Direction of the sort can be defined by using the argument *ascending = True/False* in the .sort_values() method. Sorting by mulitple columns and selecting the sort direction can be done by passing a list to the ascending field in the method argument:

        df.sort_values("*arg*",
            ascending = *True*)

        df.sort_values(["*arg[0]","arg[1]*"], 
            ascending = [True,False])
***
Selecting a column or set of columns can be done passing a single column name to the DataFrame in square brackets or a list of columns in the square brackets:

        df['column']
        
        df[['column1','column2']]
***
Boolean conditions within the first square brackets can be used to subset the DataFrame to filter data based on interest(s). Multiple Boolean conditions can be used via logical operators and(&) and or(|):

        df[df['column'] == 'value within column']

        df[(df['column1'] == 'value within column1') & (df['column2'] == 'value within column2')]
***

If multiple values are of interest to filter a column, use the *.isin() method with a list of values:

        df[df['column1'].isin(['value1 within column1','value2 within column1'])]
***

- [x] Sorting
  - Use homelessness.sort_values("individuals") to sort the entire dataframe based on the individuals columns
- [x] Subsetting Columns
  - To view only the individuals column, select the column via homelessness["individuals"]
  - To view multiple columns of state and family_members, provide a list like ["state","family_members] to select within the homelessness DataFrame
- [x] Subsetting Rows
  - Subsetting rows of interest is done by adding a Boolean statement into the square brackets. Selecting rows where homelessness exceeds 10000 individuals is done by the following code:

            homelessness[homelessness["individuals"]>10000]
- [x]  New Columns
  - This is done by attempting to select a column that doesn't exist. This will initiate a new column

## 2. Aggregating DataFrames

**DataFrame: sales**
*Index(['store', 'type', 'department', 'date', 'weekly_sales', 'is_holiday', 'temperature_c', 'fuel_price_usd_per_l', 'unemployment'], dtype='object')*

- [x] Summary Statistics
  - Selecting a column and using *.mean(), .mode(), .median(), .min(), .max(), .std(), and .var()* work to provide statistical data for a specific column or columns

***
Use the *.agg()* method, which means aggregate, to pass a function or functions to compute/handle an entire column or columns:

        df["column"].agg(*function_name*)
        df[["column1","column2"]].agg(*function_name*)

        df["column"].agg(*function_name1*,*function_name2*)
        df[["column1","column2"]].agg(*function_name1*,*function_name2*)
***
Cumulative statistics can be performed on an entire column or columns and cumulatively increment methematical operations down the rows. These functions return an entire column:

        #cumulative sum
        df["column"].cumsum()

        #cumulative product
        df["column"].cumprod()

         #cumulative max
        df["column"].cummax()
***

    - Mean and Median
    - Summarizing Dates
    - Efficient Summaries  
    - Cumulative Statistics

- [x] Counting
  - Dropping Duplicates
  - Counting Categorical Variables
- [x] Grouped Summary Statistics
  - Grouping
  - Calcaultions after Grouping
  - Multiple Groupedz Summaries
- [x] Pivot Tables
  - Pivoting on one Variable
  - Filling in Missing Values and Sum Values

## 3. Slicing and Indexing DataFrames

- [x] Explicit Indexes
  - Setting and Removing Indexes
  - Subsetting with .loc[]
  - Setting Multi-level Indexes
  - Sorting by Index Values
- [x] Slicing and Subsetting with .loc and .iloc
  - Slicing Index Values
  - Slicing in Both directions
  - Slicing Time Series
  - Subsetting by Row/Column Number
- [x] Working with Pivot Tables
  - Pivoting by Column
  - Subsetting Pivot Tables
  - Calculating on a Pivot Table 

## 4. Creating and Visualizing DataFrames

**DataFrame : avocados : [1014 rows x 6 columns]**
*Index(['date', 'type', 'year', 'avg_price', 'size', 'nb_sold'], dtype='object')*

- [x] Visualizing Data
  - Bar Plots for Categorical Data
    - For each avocado size group, calculate the total number sold, storing as nb_sold_by_size.
    - Create a bar plot of the number of avocados sold by size.
  - Line Plots for Data over Time
    - For each date, calculate the total number sold, storing as nb_sold_by_date.
    - Create a line plot of the number of avocados sold on each date
  - Scatter Plots for Numerical Data Comparison
    - Create a scatter plot to establish relationship between cost of avocados and number sold
  - Histogram for Comparison of Numerical Data that belongs to Different Types
    - Establish two histograms that overlap based on type of avocado (conventional vs organic) and adjust opacity
- [x] Missing Values
  - Finding Missing Values
  - Removing Missing Values
  - Replacing Missing Values

***
To produce a boolean DataFrame of the current DataFrame that displays *True* or *False* if a value is missing from the DataFrame

        df.isna()
***
Using *.isna()* with *.any()* in conjuction will produce a table based on if there are any missing values present in a specific column

        df.isna().any()
***
Further adding *.sum()* in conjunction will produce a sum of *True* values, which can further plotted with the *.plot()* method

        df.isna().any().sum()
***

- [x] Creating Dataframes
  - List of Dictionaries
  - Dictionary of Lists
- [x] Reading and Writing CSVs
  - CSV to DataFrame
  - DataFrame to CSV

Practice datasets:

1. [netflix_titles.csv](https://www.kaggle.com/datasets/shivamb/netflix-shows)
