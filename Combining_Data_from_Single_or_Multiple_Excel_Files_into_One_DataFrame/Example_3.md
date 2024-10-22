# Consolidating Data from Multiple Excel Sheets into a Single Table with Sheet Identification

The objective of this code is to read all the sheets from an Excel file (`Input_File.xlsx`), combine them into a single DataFrame, and add a new column called 'Sheet' to identify which sheet each row came from. It is designed to merge data from multiple sheets into one consolidated table for easier analysis.

## Import Required Libraries


```python
# Import Libraries
import os
import pandas as pd
```

## Set Input File Path


```python
# Set Excel Sheet Path
folder_path = 'D:/merge'
os.chdir(folder_path)
```

## Import Excel Sheet


```python
# Read all tabs into a single DataFrame
df = pd.read_excel('Input_File.xlsx', sheet_name=None)
```

## Merge All Sheets into a Single DataFrame with Sheet Name as a Column


```python
# Merge all sheets into a single DataFrame, adding a 'Sheet' column with the sheet name
df0 = pd.concat([d.assign(Sheet=s) for s, d in df.items()], ignore_index=True)
```


```python
df0
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Id</th>
      <th>Sheet</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Umer</td>
      <td>1</td>
      <td>PHD</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ali</td>
      <td>2</td>
      <td>BS</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ahmed</td>
      <td>3</td>
      <td>MS</td>
    </tr>
  </tbody>
</table>
</div>


