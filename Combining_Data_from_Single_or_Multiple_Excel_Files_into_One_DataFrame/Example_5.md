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


# Merging Data from Multiple Excel Files into DataFrames by Sheet

In many data analysis tasks, it is common to work with multiple Excel files that contain related data across different sheets. This example provides a comprehensive approach to merging data from all Excel files in a specified directory. By reading each Excel file and combining the data from all sheets into a single DataFrame, we can easily analyze and visualize the consolidated dataset. The method also includes additional columns for the sheet name and file name, allowing for better traceability and understanding of the data sources.



![](https://github.com/Umersaeed81/Pands-/blob/main/Combining_Data_from_Single_or_Multiple_Excel_Files_into_One_DataFrame/Example_5.png?raw=true)

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


## Explanation
This example is similar to the [previous](https://github.com/Umersaeed81/Pands-/blob/main/Combining_Data_from_Single_or_Multiple_Excel_Files_into_One_DataFrame/Example_4.md) one; however, in this example, we also retrieve the sheet name and the full file name. By adding two new columns—one for the sheet name and another for the file name—we achieve a consolidated view of the data from multiple Excel files and their respective sheets, making it easier to analyze the combined data.


![](https://github.com/Umersaeed81/File_Management_Operations/blob/main/log/banoqabil.png?raw=true)


