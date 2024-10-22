# Merging Multiple Excel Files by Sheet Name into a Single DataFrame

The goal of this code is to merge all Excel files from a specified directory into a single DataFrame for each sheet in those files. It reads all the sheets from the first Excel file, combines the data from the same sheets across all the specified files, and adds two new columns: one indicating the sheet name and another showing the original filename.

## Import Required Libraries


```python
# Import Libraries
import os
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
    

## Merging Excel Sheets with File Name Extraction


```python
df0 = {s: pd.concat(
            (pd.read_excel(f, sheet_name=s)
             .assign(Sheet=s, File=os.path.basename(f)) 
             for f in df), 
            ignore_index=True
        ) for s in sheets}
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
      <th>Sheet</th>
      <th>File</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Umer</td>
      <td>1</td>
      <td>PHD</td>
      <td>Input_File.xlsx</td>
    </tr>
    <tr>
      <th>1</th>
      <td>US</td>
      <td>11</td>
      <td>PHD</td>
      <td>Input_File_1.xlsx</td>
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
      <th>Sheet</th>
      <th>File</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ahmed</td>
      <td>3</td>
      <td>MS</td>
      <td>Input_File.xlsx</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AAS</td>
      <td>13</td>
      <td>MS</td>
      <td>Input_File_1.xlsx</td>
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
      <th>Sheet</th>
      <th>File</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ali</td>
      <td>2</td>
      <td>BS</td>
      <td>Input_File.xlsx</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AS</td>
      <td>12</td>
      <td>BS</td>
      <td>Input_File_1.xlsx</td>
    </tr>
  </tbody>
</table>
</div>


