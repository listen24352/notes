[TOC]

# openpyxl


## 1.安装

```python
pip install openpyxl
pip install lxml
```

## 2.打开与保存

### 新建

```python
from openpyxl import Workbook

# 新建Excel
wb = Workbook()
# 保存
wb.save('./wb.xlsx')
```

### 保存

```python
import os.path
from openpyxl import Workbook
wb = Workbook()

path = "./excel_ files/aa"  # 不包含文件名的文件路径
file_name = "test.xlsx"  # 文件名
file_path = os.path.join(path,file_name)  # 拼接文件路径和文件名
print( file_path)  # 输出：./excel_ files\test.xlsx

# 如果文件路径不存在则新建
if not os.path.exists(path):
    os.makedirs(path)
wb.save( file_path)
```

### 打开工作簿

```python
# 打开工作簿
from openpyxl import load_workbook

lw = load_workbook('discipline.xlsx')
```

## 3.操作工作表

```python
from openpyxl import Workbook, load_workbook


def hr():
    print("_" * 100)


# 1获取默认工作表
wb = Workbook()
ws = wb.active
print(type(ws), ws)
hr()

# 2工作表属性
lwb = load_workbook('discipline.xlsx')

# 获取第一张表
ws = lwb.active
print(ws.title)

# 修改 sheet 名
# ws.title = '计算机科学与技术'
# print(ws.title)

# 保存
# lwb.save('discipline.xlsx')

# 最大行数
print(ws.max_row)

# 最大列数
print(ws.max_column)

# 使用的矩阵范围
print(ws.dimensions)

# 编码类型
print(ws.encoding)
hr()

# 3获取工作表
# 获取表名
print(lwb.sheetnames)

# 通过表名获取工作表
s1 = lwb['计算机科学与技术']
print(s1.title)
hr()

# 4新建工作表
wb1 = load_workbook('wb.xlsx')
print(wb1.sheetnames)
new_sheet1 = wb1.create_sheet('NewSheet1', 0)
new_sheet2 = wb1.create_sheet('NewSheet2')
print(f'wb1.sheetnames:{wb1.sheetnames}')
print(new_sheet1.title)
print(new_sheet2.title)
hr()

# 5删除工作表
wb1.remove(new_sheet1)
print(wb1.sheetnames)


# 6移动工作表
Workbook().move_sheet("Sheet1", -1)

# 7复制工作表
Workbook().copy_worksheet(wb.active)
```

## 4.访问单元格

```python
from openpyxl import Workbook, load_workbook
from openpyxl.utils import rows_from_range
import pprint


def hr():
    print("_" * 100)


# 1获取单个单元格
wb = Workbook()
ws = wb.active

cell1 = ws["a6"]  # 通过坐标获取
cell2 = ws.cell(1, 2)  # 通过行列下标获取
cell3 = ws.cell(2, 5, "test value")  # 通过行列下标获取
print(type(cell1))  # 输出：<class 'openpyxl.cell.cell.Cell'>
print(type(cell2))  # 输出：<class 'openpyxl.cell.cell.Cell'>
print(type(cell3))  # 输出：<class 'openpyxl.cell.cell.Cell'>

# 2单元格属性
# 3修改单元格
# from openpyxl import Workbook
# wb = Workbook()
# ws = wb.active
# i = 1
# for x in range(1,11):
#     for y in range(1,21):
#          ws.cell(x,y,i)
#          i += 1
# wb.save("test.xlsx")

hr()
# 4获取多个单元格
wb = load_workbook('test.xlsx')
ws = wb.active
# 选取第2行(下标从1开始),返回一个元祖
row_cells = ws[2]
print(row_cells)

# 选取A列，返回一个元组
col_cells = ws['B']
print(col_cells)

# 选取2、3、4行
rows_range_cells = ws[2:4]
print(rows_range_cells)

# 选取B、C、D共3列
col_range_cells = ws["B:D"]
# pprint.pprint(col_range_cells)
print(col_range_cells)

# 选取c3到f6区域
range_cells = ws["c3:f6"]
print(range_cells)

hr()
from openpyxl.utils import get_column_letter, column_index_from_string

# 数字转字母
col_letter = get_column_letter(1)
print(col_letter)

# 字母转数字
col_idx = column_index_from_string(col_letter)
print(col_idx)
hr()
wb = load_workbook('test.xlsx')
ws = wb.active
# 前4个参数分别是最小列、最大列、最小行、最大行，
cells = ws.iter_rows(min_col=2, max_col=5, min_row=1, max_row=3)
for cell in cells:
    print(cell)

# 第5个参数是values_only，表示是否只取值
cells = ws.iter_rows(min_col=2, max_col=5, min_row=1, max_row=3, values_only=True)
for cell in cells:
    print(cell)

#
for cells in ws.rows:
    print(cells)
hr()
for cells in ws.columns:
    print(cells)
hr()
for rows in ws.values:
    for value in rows:
        print(value)
```

## 5.操作单元格

## 6.使用公式

## 7.设置样式

## 8.过滤和排序

## 9.插入图表

## 10.只读只写

## 11.加密保护

## 12.xls转xlsx
