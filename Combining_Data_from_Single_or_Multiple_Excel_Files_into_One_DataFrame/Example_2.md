# Example-2

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
