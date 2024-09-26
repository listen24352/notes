# Pandas

## 安装

```python
pip install pandas
```

## 读取Excel

```python
import pandas as pd
book_data = pd.read_excel('test.xlsx')

# 返回总的行列数
rows, cols = book_data.shape
print(rows, cols)

# 以列表格式返回第一行数据
# iloc['第几号数据']
rows_list = book_data.iloc[0].tolist()
print(rows_list)

# 以列表格式返回第一列数据
# book_data['列名']
column_list = book_data[1].tolist()
print(f'column_list{column_list}')
```

