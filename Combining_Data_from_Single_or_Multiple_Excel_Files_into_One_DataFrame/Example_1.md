# Merging All Sheets from an Excel File into a Single DataFrame

The objective of this code is to:

1. **Read all the sheets** from an Excel file (`Input_File.xlsx`) into separate dataframes.
2. **Combine** (or merge) all these sheets into one single dataframe.

In simple terms, the code collects data from every tab in the Excel file and merges it all together into one big table for easier analysis.

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

## Merge All Sheets into Single DataFrame


```python
# Merge all sheets into a single DataFrame
df0 = pd.concat(df.values(), ignore_index=True)
```


```python
df0
```





<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Umer</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ali</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ahmed</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



## Export Output


```python
df0.to_excel('Merged.xlsx',index=False)
```

## Explanation
- The `pd.read_excel()` function is used with `sheet_name=None` to read all the sheets from the specified Excel file into a dictionary of dataframes. Each key in the dictionary corresponds to a sheet name, and the value is the respective dataframe containing the data from that sheet.
- The `pd.concat()` function is then called on the values of this dictionary to concatenate all the individual dataframes into a single dataframe (`df0`). The `ignore_index=True` parameter resets the index in the new combined dataframe, providing a continuous index from 0 to n-1, where n is the total number of rows in the combined dataframe.
