Here's a comprehensive cheatsheet for **Pandas**—one of the most important Python libraries for data manipulation and analysis. This guide covers the most frequently used functionalities and methods.

### **Pandas Cheatsheet**

#### **1. Basics of Pandas**

- **Importing Pandas**:
    ```python
    import pandas as pd
    ```

- **Creating a DataFrame**:
    ```python
    data = {'col1': [1, 2, 3], 'col2': [4, 5, 6]}
    df = pd.DataFrame(data)
    ```

- **Creating a Series**:
    ```python
    series = pd.Series([1, 2, 3, 4])
    ```

- **Reading Data**:
    ```python
    df = pd.read_csv('file.csv')  # From a CSV file
    df = pd.read_excel('file.xlsx')  # From an Excel file
    df = pd.read_sql('SELECT * FROM table', connection)  # From SQL
    ```

- **Exporting Data**:
    ```python
    df.to_csv('file.csv')  # Save to CSV
    df.to_excel('file.xlsx')  # Save to Excel
    ```

#### **2. Data Inspection**

- **View First/Last Rows**:
    ```python
    df.head()  # First 5 rows
    df.tail()  # Last 5 rows
    ```

- **Dataframe Info**:
    ```python
    df.info()  # Column info, null counts, types
    df.describe()  # Summary statistics
    ```

- **Accessing Specific Rows/Columns**:
    ```python
    df['col1']  # Access a column
    df[['col1', 'col2']]  # Access multiple columns
    df.iloc[0]  # First row by position
    df.loc[0]  # First row by index label
    ```

#### **3. Data Selection and Filtering**

- **Filtering Data**:
    ```python
    df[df['col1'] > 2]  # Rows where col1 > 2
    df[df['col1'].isin([1, 2])]  # Rows where col1 is in the given list
    ```

- **Using `.loc[]` for Label-based Selection**:
    ```python
    df.loc[0, 'col1']  # Access specific cell by row label and column label
    df.loc[:, 'col1']  # All rows, 'col1' column
    ```

- **Using `.iloc[]` for Position-based Selection**:
    ```python
    df.iloc[0, 0]  # Access first row, first column (by index)
    ```

#### **4. Data Cleaning and Transformation**

- **Renaming Columns**:
    ```python
    df.rename(columns={'col1': 'new_col1'}, inplace=True)
    ```

- **Handling Missing Data**:
    ```python
    df.isnull()  # Returns a DataFrame of booleans
    df.dropna()  # Drop rows with any missing values
    df.fillna(0)  # Fill missing values with 0
    ```

- **Dropping Columns or Rows**:
    ```python
    df.drop(columns=['col1'])  # Drop specific columns
    df.drop(index=[0])  # Drop specific rows by index
    ```

- **Changing Data Types**:
    ```python
    df['col1'] = df['col1'].astype(float)  # Convert column to float
    ```

- **Applying Functions**:
    ```python
    df['col1'] = df['col1'].apply(lambda x: x * 2)  # Apply function to a column
    ```

#### **5. Data Aggregation and Grouping**

- **Group by**:
    ```python
    df.groupby('col1').sum()  # Group by 'col1' and get sum of each group
    df.groupby('col1')['col2'].mean()  # Mean of 'col2' for each 'col1'
    ```

- **Aggregating Data**:
    ```python
    df.aggregate(['sum', 'mean'])  # Apply multiple aggregate functions
    ```

#### **6. Sorting and Ranking**

- **Sort Values**:
    ```python
    df.sort_values(by='col1', ascending=False)  # Sort by column
    df.sort_values(by=['col1', 'col2'], ascending=[True, False])  # Multiple columns
    ```

- **Ranking Data**:
    ```python
    df['rank'] = df['col1'].rank()  # Rank the values in a column
    ```

#### **7. Merging and Joining DataFrames**

- **Merge DataFrames**:
    ```python
    pd.merge(df1, df2, on='col1')  # Merge on 'col1'
    pd.merge(df1, df2, how='left', on='col1')  # Left join
    ```

- **Concatenate DataFrames**:
    ```python
    pd.concat([df1, df2], axis=0)  # Stack DataFrames vertically
    pd.concat([df1, df2], axis=1)  # Concatenate DataFrames horizontally
    ```

#### **8. Date and Time Operations**

- **Convert Strings to Dates**:
    ```python
    df['date'] = pd.to_datetime(df['date'])  # Convert to datetime
    ```

- **Extract Date Components**:
    ```python
    df['year'] = df['date'].dt.year  # Extract year
    df['month'] = df['date'].dt.month  # Extract month
    ```

- **Date Ranges**:
    ```python
    pd.date_range(start='2024-01-01', end='2024-12-31', freq='D')  # Daily date range
    ```

#### **9. Pivot Tables**

- **Creating Pivot Table**:
    ```python
    df.pivot_table(values='value', index='category', columns='date', aggfunc='sum')
    ```

#### **10. Visualization (using Pandas + Matplotlib)**

- **Plotting Data**:
    ```python
    df['col1'].plot()  # Plot a single column
    df.plot(x='col1', y='col2', kind='scatter')  # Scatter plot
    df.plot(kind='hist', bins=10)  # Histogram
    ```

- **Customizing Plots**:
    ```python
    df['col1'].plot(title='Column 1')  # Adding title
    ```

#### **11. Miscellaneous**

- **Get unique values in a column**:
    ```python
    df['col1'].unique()  # Get unique values in 'col1'
    ```

- **Get value counts**:
    ```python
    df['col1'].value_counts()  # Frequency of unique values in 'col1'
    df['col1'].value_counts(normalize=True, sort=True)  # Proportion of unique values in 'col1'
    ```

- **Concatenating Series**:
    ```python
    pd.concat([series1, series2], axis=0)  # Concatenate two Series
    ```

---

This cheatsheet includes the most commonly used features in Pandas to help with data wrangling, exploration, and analysis. Keep in mind that Pandas also integrates well with libraries like **NumPy**, **Matplotlib**, and **Seaborn** for more advanced analysis and visualization.