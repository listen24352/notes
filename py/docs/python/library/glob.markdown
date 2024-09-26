# 文件通配符

```python
import os
import glob


# os.makedirs('test/a')
# 返回list
print(glob.glob('*.py'))

# 返回iterator
print(list(glob.iglob('*.py')))
# print(next(glob.iglob('*.py',recursive=True)))

# 转义所有特殊字符 ('?', '*' 和 '[')。
# 例如在 Windows 上 escape('//?/c:/Quo vadis?.txt') 将返回 '//?/c:/Quo vadis[?].txt'。
# print(glob.escape(''))

print(glob.glob('./[0-9].*'))

print(glob.glob('*.gif'))

print(f'?:{glob.glob("?.*")}')

print(glob.glob('**/*.txt', recursive=True))

print(glob.glob('./**/', recursive=True))

print(glob.glob('.c*'))


# print('_' * 10)


# # 假设我们有一个包含特殊字符的文件路径
# path_pattern = "[special]/file*.txt"
#
# # # 使用 glob.escape 转义特殊字符
# escaped_pattern = glob.escape(path_pattern)
# print(escaped_pattern)
```

