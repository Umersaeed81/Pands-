<table style="border-collapse: collapse;">
  <tr>
    <td style="vertical-align: top;">
      <h1><a href="https://www.linkedin.com/in/engumersaeed/">Umer Saeed</a></h1>
      Sr. RF Planning & Optimization Engineer<br>
      BSc Telecommunications Engineering, School of Engineering<br>
      MS Data Science, School of Business and Economics<br>
      <strong>University of Management & Technology</strong><br>
      <strong>Mobile:</strong> +923018412180<br>
      <strong>Email:</strong> umersaeed81@hotmail.com<br>
      <strong>Address:</strong> Dream Gardens, Defence Road, Lahore<br>
    </td>
    <td style="vertical-align: top; padding-left: 100px;">
      <img src="https://github.com/Umersaeed81/File_Management_Operations/blob/main/log/banoqabil.png?raw=true" alt="Bano Qabil Logo" width="500"/>
    </td>
  </tr>
</table>

# Combining Data from Matching Sheet Names Across Multiple Excel Files

The objective of this code is to:

1. Import all Excel files from the folder `'D:/merge/'`.
2. Identify all the sheet names in the first Excel file.
3. Combine the data from each sheet across all the Excel files into one single dataset for each sheet, merging the data vertically (row by row).
4. Ignore the original row indices, and create new ones for the combined data.

![](https://github.com/Umersaeed81/Pands-/blob/main/Combining_Data_from_Single_or_Multiple_Excel_Files_into_One_DataFrame/Example_4.png?raw=true)

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

![](https://github.com/Umersaeed81/File_Management_Operations/blob/main/log/banoqabil.png?raw=true)
