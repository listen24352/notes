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

## demo

```python
import os
from datetime import datetime
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent

LOG_DIR = BASE_DIR / 'log'

from selenium import webdriver


def get_log_path_and_name():
    """
    根据当前日期生成日志文件夹和文件名，并返回日志文件的完整路径（字符串形式）
    """
    now = datetime.now()
    log_dir = LOG_DIR / f"{now.year}-{now.month:02d}"
    if not os.path.exists(log_dir):
        os.makedirs(log_dir)
    log_file = log_dir / f"{now.year}-{now.month:02d}-{now.day:02d}.log"
    return str(log_file)

if __name__ == '__main__':
    log_path = get_log_path_and_name()
    print(log_path)

# service = webdriver.ChromeService(service_args=['--append-log', '--readable-timestamp'],
#                                   log_output=get_log_path_and_name())
#
# driver = webdriver.Chrome(service=service)
# driver.get('https://www.baidu.com')

```

