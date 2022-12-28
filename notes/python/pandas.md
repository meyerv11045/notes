# Pandas

- [Corey Schafer Playlist](https://www.youtube.com/playlist?list=PL-osiE80TeTsWmV9i9c58mdDCSskIFdDS)

## dataframe basics

- `df.shape`, `df.info()`

- `pd.set_option('display.max_columns', 86)` in jupyter notebook to be able to scroll through all the columns

- `df.head(10)`  or `df.tail()` (number is optional # of rows to see)

- dataframes can be thought of as python dictionaries with enchanced functionality

    ``` python
    {
    	"col1": ['row1 val', 'row2 val', ...],
     	"col2": ['row1 val', 'row2 val', ...],
      ...
    }
    ```

- column in a dataframe is a `Series` object where all the elements are values specific to a sample

    - `df.columns`

- df is a container for multiple series objects 

- `df['email']` is equivalent to `df.email` but former is safer/best practice for accessing a single column

- `df[['col1', 'col2']]` for accessing multiple columns

    - must be a list of cols passed to `df[]`
    - no longer returns a series

## iloc

- access row by integer location `df.iloc[0]` returns a series corresponding to the 1st row
- can get multiple rows by integer location by passing a list of row indices `df.iloc[[0,1]]` (no longer returns a series)
- can also access columns by integer index (not names) by passing as second param: `df.iloc[[1,2], 1]`
- can use slicing to select multiple rows/cols
    - `start:end` (inclusive)
    - `df.loc[0:2]` selects the first 3 rows
    - `df.loc[:, 1]` selects all rows for col 1

## loc

- access row/col by the label for the specific axis
    - for columns, it would be the column name
    - for rows, by default it would be the integer index (but the row label could be modified to be something else)
- `df.loc[[0,1], ['name', 'email']]` gets the name and email for the first two rows

## simple stats

- `df['col'].value_counts()` gives counts for each class of categorical categorical data
    - `normalize=True` to get percentages
- `df.describe()`

## indexes

- `df.set_index('col')`
    - is not inplace by default. (must set `inplace=True`)
    - integers are no longer the default index for the rows (can still use `iloc[0]` but cannot use `loc[0]`)
- `df.reset_index(inplace=True)`
- Can set index as you load in the data using: `df.read_csv('filename.csv', index_col='col_name')`
- `df.sort_index(ascending=False, inplace=True)` 

## filtering

- [YT Vid](https://www.youtube.com/watch?v=Lw2rlcxScZY)
- `filter = df['name'] == 'Doe'` is a boolean series. 
    - acts as a filter mask (rows that the condition is true have a true value)
    - `df[filter]` returns the resulting dataframe with the filter applied
    - `df.loc[filter]` also applies the filter to the dataframe and returns a copy of it
        - lets you easily select columns from the filtered data `df.loc[filter, 'emmail']`
- `filter = (df['last'] == 'Doe') & (df['salary'] > 65000)`
    - can use `&`, `|`, and `~` (not) boolean operators in a filter

```python
countries = ['US', 'India', 'UK', 'Canada']
filter_ = df['Country'].isin(countries)
```

- `filter = df['Skills'].str.contains('Python', na=False)`
    - python is in the skills section which is just a big string
    - handles NaNs by just skipping them 
    - str methods are very useful for data processing

## updating rows/cols

- `df.columns = [x.lower() for x in df.columns]` will update *all* the column names
    - `df.columns.str.replace(' ', '_')` for replacing spaces with underscores to be compatible with dot notation
- `df.rename(columns={'first_name': 'first', 'last_name': 'last'}, inplace=True)` for updating only specific columns using a dict mapping current name to new name
- `df.loc[row_idx, ['col1','col5']] = [val1, val5]` for updating specific cols in a row

### apply

- `df['col'] = df['col'].apply(func)` where func is any function that takes in the current row value and outputs the updated row value
- `df.apply(pd.Series.min)` displays the min item for each column

### applymap

- `df.applymap(func)` applies a function to every element of a dataframe

### map

- `df['first'].map({"Jane": "Mary", "Chris": "Corey"})` returns a col with the specified mapping applied
    - note: all the possible values must be specified or they will be mapped to NaN
    - `replace()` does not map unspecified values to NaN
- useful for turning yes/no responses to booleans `df['col'].map({'Yes': True, 'No': False})`

## add/drop rows/cols

- `df.drop(columns=['col1', 'col2'], inplace=True)` to remove columns
- `indices = df[filter].index` gives us the indices of the rows to be dropped so we can do `df.drop(index=indices)`
- `df.dropna()` to drop all rows that contain `NaN` in any of the columns

## sorting

- `df.sort_values(by='col')` and set `ascending=False` to get descending order. another `inplace=True` one
- `df.sort_index()`
- `df.nsmallest(n, 'col')` and `df.nlargest` give the n smallest/largest values in the column with their corresponding rows in the dataframe
- `df['col'].nsmallest(n)` gives just the n smallest values in the column

## grouping

``` python
country_grp = df.groupby(['Country'])
country_grp.get_group('United States') # returns a df where all the Country values = US
```



## data cleaning



## data pipes

- clean readable way of processing your data
- (+) a single function can perform a single operation
    - functions should not do inplace operations on the dataframe
- by default modifies the df it is called on unless on of the functions creates a copy of the dataframe
- [Method Chaining & Pandas Pipe](https://tomaugspurger.github.io/method-chaining)
- [Pandas Pipe](https://sinyi-chou.github.io/python-pandas-pipe/)



## mocking dataframes

``` python

import pandas as pd
from faker import Faker

# Create an Faker object
fake = Faker()

# Now you have many options to genarate data:
fake.name()
fake.text()
fake.address()
fake.email()
fake.date()
fake.country()
fake.phone_number()
fake.random_number(digits=5)

# let's generate an example DataFrame
faker_df = pd.DataFrame({'date':[fake.date() for i in range(10)],
                         'name':[fake.name() for i in range(10)],
                         'email':[fake.email() for i in range(10)],
                         'text':[fake.text() for i in range(10)]})
faker_df
```

## df prelim analysis

``` python
def analyse_df(df, corr_limit = 0.75):
    """Analyse any dataframe and print results
    * Print df Shape, duplicate rows qnt, memory usage, data types and call DataFrame.describe()
    * Check Missing values in each columns, returning qnt. and percentage 
    * Check Linear Correlation between columns, return Pearson number
    Keyword arguments:
    df -- Any DataFrame
    corr_limit -- Correlation Limit (Pearson) to define if relationship exists (default 0.75)
    """   

    print('General Info:')
    print(f'{df.shape[0]} Rows {df.shape[1]} Columns'
          f'\n{df.duplicated().sum()} Duplicated Rows'
          f'\nMemory Usage: {df.memory_usage().sum()/(1024*1024):.2f}Mb')
    
    # Checking Data Types
    int_list, float_list,object_list,bool_list,other_list =[[] for i in range(5)]
    for col in df.columns:
        if df[col].dtype == 'int64':
            int_list.append(col)
        elif df[col].dtype == 'float64':
            float_list.append(col)
        elif df[col].dtype == 'object':
            object_list.append(col)
        elif df[col].dtype == 'boolean':
            bool_list.append(col)
        else:
            other_list.append(col)
            
    for type_list,data_type in zip([int_list, float_list,object_list,bool_list,other_list],
                                   ['int64','float64','object','boolean','other']):
        if len(type_list)>0:
            print(f'\nColumns {data_type}: {type_list}')
            
    # General statistics
    display(df.describe())
    
    # Checking Missing Values in each columns
    print('\nCheking Missing Values:')
    col_with_missing_counter = 0
    for col in df.columns:
        qnt_missing = df[col].isna().sum()
        if qnt_missing > 0:
            col_with_missing_counter +=1
            print(f'Column "{col}" has {qnt_missing} missing values ({qnt_missing/df.shape[0]:.2%})')
    if col_with_missing_counter ==0 :
        print('Analyzed DataFrame has no missing values')
        
    # Checking linear correlation between columns
    print('\nChecking Linear Correlation:')
    df_corr = df.corr() # Correlation DataFrame
    ckecked_list =[] # Ensure that we won't print the same information twice
    cols_with_correlation_counter = 0
    for col in df_corr.columns:
        ckecked_list.append(col)
        for i in range(len(df_corr)):
            if ((df_corr[col][i] > corr_limit or df_corr[col][i] < -corr_limit) and
                (df_corr.index[i] not in ckecked_list)):
                cols_with_correlation_counter += 1
                print(f'Linear Correlation found between columns '
                      f'{df_corr.index[i]} and {col} -> Pearson coef. = {df_corr[col][i]:.2f}')         
    if cols_with_correlation_counter == 0:
        print('No linear correlation was found')
```

