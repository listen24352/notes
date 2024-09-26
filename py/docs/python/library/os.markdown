# 操作系统接口-OS


---

==模块提供了许多与操作系统交互的函数==

```python
import os

# 查看当前文件目录
print(os.getcwd())

# 切换目录
os.chdir(r'C:\Users\Admin\Desktop')

print(os.getcwd())

# 列出当前目录下的所有文件
print(os.listdir())

# 创建一个目录
os.mkdir('test')

# 删除目录
os.rmdir('test')

# 递归创建
os.makedirs('a/b/c', exist_ok=True)

# 递归删除
os.removedirs('a/b/c')

# 删除文件
os.remove('./1.py')

# 重命名文件
os.rename('original_file.txt', 'renamed_file.txt')
```

