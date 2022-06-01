# Datacamp Pandas Curricula

practicing pandas based on datacamp videos with various datasets

## Data Manipulation with Pandas

### 1. Transforming DataFrames

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

### 2. Aggregating DataFrames

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

### 3. Slicing and Indexing DataFrames

**DataFrame: temperatures**
*Index(['date', 'city', 'country', 'avg_temp_c'], dtype='object')*

- [x] Explicit Indexes
  - Setting and Removing Indexes
    - Set the index or indexes using *.set_index()*. Multiple arguments can be used in list format for the method for multi-level indexing
    - Reset the index in two ways:
      1. Maintaining the current DataFrame using *.reset_index()*
      2. Reseting the DataFrame to the initial ordering using *.reset_index(drop = True)*

***
Setting the index or indexes

        temperatures.set_index('date')

Multi-level indexing using a list of columns

        temperatures.set_index(['date','avg_temp_c'])

***

Resetting the index or indexes

        temperatures.reset_index()
        
        temperatures.reset_index(drop = True)
***

- Subsetting with .loc[]
- Sorting by Index Values
  - Sort the index or indexes using *.sort_index()* method on a DataFrame.
  - If multiple indexes are available, *level* argument may be used to pick which goes first. *level* is assigned with a list of the indexes
  - Use *ascending* and assign boolean value(s) to sort direction and match with a list of booleans to the levels used

***
This will only sort the top-most index

        temperatures.sort_index()

This statement can sort inner indexes as the priority sort

        temperatures.sort_index(level = 'city')

This statement will sort by 'country' column and then by 'city'. Note the order of ascending

        temperatures_ind.sort_index(level = ['country','city'],ascending = [True,False])

***

- [x] Slicing and Subsetting with .loc and .iloc
  - Slicing Index Values
    - Slice rows by using the loc function to slice by index, at the outer-most level
    - Inner level slicing requires a tuple of the outer to inner list: *[('outer-index':'inner-index')]* with the loc function
  - Slicing in Both directions
    - Slicing columns relies on using the loc function, but with a comma to associate with row:column pairing: *[('outer-index':'inner-index'):('outer-column':'inner-column')]*
      - The index portion of the loc function can be omitted to only slice columns
  - Slicing Time Series

***

After setting the indexes to 'country' and 'city':
This first loc call subsets for the outer index, all 'country' in the DataFrame are subset for Pakistan to Russia, inclusive of the alphabetical countries in between in the DataFrame

        temperatures.loc['Pakistan':'Russia']

This next loc call will subset the DataFrame based on all 'country' and 'city' values in between the selected countries and cities, alphabetically

        temperatures.loc[('Pakistan','Lahore'):('Russia','Moscow')]

        temperatures.loc[("India","Hyderabad"):("Iraq", "Baghdad")]

Calling loc without the indexes selected, but with columns selected will subset the DataFrame based on the columsn

        temperatures.loc[:,"date":"avg_temp_c"]

Adding the index selections will then subset both the rows and columns appropriately

        temperatures.loc[("India","Hyderabad"):("Iraq", "Baghdad"),"date":"avg_temp_c"]

***

- [x] Working with Pivot Tables
  Create a pivot table from the DataFrame using the *.pivot_table() method
  Arguments for this method include:
  1. *values* which are selected values of interest
  2. *columns* which are the column or columns (via list) that we want to use as columns in the pivot table
  3. *index* which is like *columns* will take a value or list of values that should be used to index the pivot table

  - Pivoting by Column

***
Creates a pivot table that has index values based on the country and city, columns that are each year, and average temperature values as the content of the row:column pairing

      temp_by_country_city_vs_year = temperatures.pivot_table(values= 'avg_temp_c', columns = 'year', index = ('country','city'))
***

- Subsetting Pivot Tables
  - Subset the pivot table using the same technique as subsetting a DataFrame
- Calculating on a Pivot Table
  -Calculations are done on each column with traditional functions like *.mean()* or *.max()*

### 4. Creating and Visualizing DataFrames

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
    *pd.DataFrame('list')*
    *pd.DataFrame('dictionary')*

  - List of Dictionaries
  - Dictionary of Lists

***
Create a list of dictionaries with new data

      avocados_list = [{"date": "2019-11-03", "small_sold": 10376832,"large_sold": 7835071},{"date":"2019-11-10", "small_sold":10717154,"large_sold": 8561348}
      avocados_2019 = pd.DataFrame(avocados_list)

Create a dictionary of lists with new data

      avocados_dict = {"date": ["2019-11-17","2019-12-01"], "small_sold": [10859987,9291631], "large_sold": [7674135,6238096]}
      avocados_2019 = pd.DataFrame(avocados_dict)

- [x] Reading and Writing CSVs
  - CSV to DataFrame
    Use *pd.read_csv('file_path')*

***

      airline_bumping = pd.read_csv("airline_bumping.csv")

***

- DataFrame to CSV
  Use *pd.to_csv('destination/name.csv')*

***

      airline_totals_sorted.to_csv("airline_totals_sorted.csv")

***
***
***
***
***

## Joining Data with Pandas

### 1. Data Merging Basics

Inner Joins/Merges:

- One-to-One Merges
- One-to-Many Merges
- Multiple Merges

### 2. Merging Tables with Different Join Types

Other Joins:

- Left Joins/Right Joins
- Outer Joins
- Self Join
- Merging on Index/Indexes

### 3. Advanced Merging and Concatenation

- Filtering Join
  - Semi-join
  - Anti-join
- Concatenation
  - Vertical join
  - Appending
- Validation/Verification

### 4. Merging Ordered and Time-Series Data

- Ordered Merge
- As Of Merge
- Queries
- Pivot Table Melt