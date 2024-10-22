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

# Collecting DataFrames from Excel Sheets into a Dictionary with Source Details

The provided code aims to read multiple Excel files from a specified directory (`D:/merge/`) and extract data from all sheets within each file. It stores the resulting dataframes in a dictionary, where each key corresponds to a sheet name, and the value is a concatenated dataframe containing data from that sheet across all Excel files. Additionally, it includes columns to indicate the source sheet and the file name from which the data was extracted.

## Important Note

In the previous example, only the sheet name of the Excel file located at the zero index (first file) is imported. Attempting to access sheets from other files without specifying the correct file location will result in an error. This behavior emphasizes the importance of managing file and sheet indexing correctly to avoid runtime errors.

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




```python
# Store dataframes for each file and sheet in a dictionary
dfs = {}

# Loop through all files
for f in df:
    # Read the Excel file
    xls = pd.ExcelFile(f)

    # Loop through each sheet in the current file
    for sheet_name in xls.sheet_names:
        # Read the sheet and apply converter for 'Integrity' and add columns for 'Sheet' and 'File'
        df_sheet = pd.read_excel(f, sheet_name=sheet_name).assign(
            Sheet=sheet_name, 
            File=os.path.basename(f)
        )
        
        # Check if the sheet name exists in the dfs dictionary
        if sheet_name in dfs:
            # If it exists, concatenate the new dataframe with the existing one
            dfs[sheet_name] = pd.concat([dfs[sheet_name], df_sheet], ignore_index=True)
        else:
            # If it doesn't exist, create a new entry in the dictionary
            dfs[sheet_name] = df_sheet
```


```python
dfs.keys()
```




    dict_keys(['PHD', 'BS', 'MS', 'PHD111'])




```python
dfs['PHD']
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
      <td>Input_File.xlsx</td>
    </tr>
  </tbody>
</table>
</div>




```python
dfs['BS']
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




```python
dfs['MS']
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
dfs['PHD111']
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
      <td>US</td>
      <td>11</td>
      <td>PHD111</td>
      <td>Input_File_1.xlsx</td>
    </tr>
  </tbody>
</table>
</div>

![](https://github.com/Umersaeed81/File_Management_Operations/blob/main/log/banoqabil.png?raw=true)
