# Merging All Sheets from Multiple Excel Files into a Single DataFrame

The objective of this code is to:

1. **Find all Excel files** in the folder D:/merge/.
2. **Read and combine** all the sheets from each Excel file.
3. **Merge the data** from all these files and their sheets into one single dataframe.

In simple terms, the code takes multiple Excel files from a folder, reads each sheet from those files, and combines everything into one big table for easier analysis.

![](https://github.com/Umersaeed81/Pands-/blob/main/Combining_Data_from_Single_or_Multiple_Excel_Files_into_One_DataFrame/Example_2.png?raw=true)

## Import Required Libraries


```python
# Import Libraries
import pandas as pd
from glob import glob
```

## Filter Excel File from the given path


```python
df1 = glob('D:/merge/*.xlsx')
df1
```




    ['D:/merge\\Input_File.xlsx', 'D:/merge\\Input_File_1.xlsx']



## Import and Concatenate Input Files 


```python
# Read all Excel files and concatenate their sheets
df2 = pd.concat(
    pd.concat(pd.read_excel(file, sheet_name=None).values())  
    for file in df1).reset_index(drop=True)
```


```python
df2
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
    <tr>
      <th>3</th>
      <td>US</td>
      <td>11</td>
    </tr>
    <tr>
      <th>4</th>
      <td>AS</td>
      <td>12</td>
    </tr>
    <tr>
      <th>5</th>
      <td>AAS</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>



## Export Output


```python
df2.to_excel('Merged.xlsx',index=False)
```

## Explanation

- The `glob()` function is used to search for all Excel files (`*.xlsx`) in the specified folder (`D:/merge/`). This returns a list of file paths for all matching files.

- A nested `pd.concat()` function is employed: the inner `pd.read_excel(file, sheet_name=None)` reads all sheets from each Excel file into a dictionary of dataframes, similar to the first example. The outer `pd.concat()` then concatenates all the sheets from each file into a single dataframe.

- Finally, the `reset_index(drop=True)` method resets the index of the combined dataframe (`df2`), ensuring a clean and continuous index without retaining the old index.
