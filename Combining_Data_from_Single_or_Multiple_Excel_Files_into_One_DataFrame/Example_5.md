# Merging Data from Multiple Excel Files into DataFrames by Sheet

The objective of the code is to merge data from all Excel files in the `D:/merge/` directory. It reads each Excel file and combines the data from all sheets into a single DataFrame for each sheet, adding two new columns: one for the sheet name and another for the file name. This way, you end up with a consolidated view of the data from multiple Excel files and their sheets.

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
    

## Combining Data from Each Sheet with Sheet and File Information Across Multiple Excel Files


```python
df0 = {s: pd.concat(
            (pd.read_excel(f, sheet_name=s).assign(Sheet=s, File=f) 
             for f in df), 
            ignore_index=True) for s in sheets}
```


```python
df0['PHD']
```





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
      <td>D:/merge\Input_File.xlsx</td>
    </tr>
    <tr>
      <th>1</th>
      <td>US</td>
      <td>11</td>
      <td>PHD</td>
      <td>D:/merge\Input_File_1.xlsx</td>
    </tr>
  </tbody>
</table>
</div>




```python
df0['BS']
```





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
      <td>D:/merge\Input_File.xlsx</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AS</td>
      <td>12</td>
      <td>BS</td>
      <td>D:/merge\Input_File_1.xlsx</td>
    </tr>
  </tbody>
</table>
</div>




```python
df0['MS']
```





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
      <td>D:/merge\Input_File.xlsx</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AAS</td>
      <td>13</td>
      <td>MS</td>
      <td>D:/merge\Input_File_1.xlsx</td>
    </tr>
  </tbody>
</table>
</div>




