# Example-1

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
