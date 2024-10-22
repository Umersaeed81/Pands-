# Combining Data from Matching Sheet Names Across Multiple Excel Files

The objective of this code is to:

1. Import all Excel files from the folder `'D:/merge/'`.
2. Identify all the sheet names in the first Excel file.
3. Combine the data from each sheet across all the Excel files into one single dataset for each sheet, merging the data vertically (row by row).
4. Ignore the original row indices, and create new ones for the combined data.

## Import Required Libraries


```python
# Import Libraries
import pandas as pd
from glob import glob
```

## Filter Excel File from the given path


```python
df = glob('D:/merge/*.xlsx')
df
```




    ['D:/merge\\Input_File.xlsx', 'D:/merge\\Input_File_1.xlsx']



## Retrieving Sheet Names from the First Excel File


```python
sheets = pd.ExcelFile(df[0]).sheet_names
print(sheets)
```

    ['PHD', 'BS', 'MS']
    

## Combining Data from Each Sheet Name Across Multiple Excel Files


```python
df0 = {s:pd.concat((pd.read_excel(f, sheet_name=s) \
        for f in df),ignore_index=True) for s in sheets}
```


```python
df0['PHD']
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
      <td>US</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
df0['BS']
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ali</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AS</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>




```python
df0['MS']
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ahmed</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AAS</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>

