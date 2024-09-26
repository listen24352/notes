# Shutil

==shutil 是 Python 的一个标准库，全称为 "shell utilities"，意为“shell 工具”。它提供了一系列对文件和文件集合进行高级操作的函数，这些操作在标准的文件操作（如使用 open() 函数读写文件）之上，提供了更为便捷和强大的功能。shutil 库主要用于文件的复制、移动、重命名、删除以及目录（文件夹）的复制和删除等操作。==

## 1.shutil.copy

<span style="color: red; font-size: 22px;">复制文件内容（不包括元数据）从源路径 src 到目标路径 dst。如果 dst 是一个目录，则文件将被复制到该目录下，并保持原名。</span>

```python
shutil.copy(src, dst, *, follow_symlinks=True)

```

## shutil.copy2

<span style="color: red; font-size: 22px;">类似于 copy()，但也会尝试保留文件的元数据（如修改时间和访问权限）。</span>

```python
shutil.copy2(src, dst, *, follow_symlinks=True)
```

## shutil.copyfile

<span style="color: red; font-size: 22px;">仅复制文件内容，不尝试保留任何元数据。如果 dst 已存在，它将被覆盖。</span>

```python
shutil.copyfile(src, dst, *, follow_symlinks=True)
```

## shutil.copyfileobj

<span style="color: red; font-size: 22px;">将一个文件对象 fsrc 的内容复制到另一个文件对象 fdst。length 参数指定了每次读取和写入操作的大小（以字节为单位）。</span>

```python
shutil.copyfileobj(fsrc, fdst, length=16*1024)
```

## shutil.copymode

<span style="color: red; font-size: 22px;">仅复制文件的权限位（不包括内容、所有者或组）。</span>

```python
shutil.copymode(src, dst, *, follow_symlinks=True)
```

## shutil.copystat

<span style="color: red; font-size: 22px;">复制文件的状态信息（如修改时间、访问时间、模式位和标志），但不复制内容、所有者或组。</span>

```python
shutil.copystat(src, dst, *, follow_symlinks=True)：
```

## shutil.move

<span style="color: red; font-size: 22px;">将文件或目录从 src 移动到 dst。如果 dst 是一个已存在的目录，则 src 将被移动到该目录下。如果 dst 是一个文件，它将被覆盖（除非 dst 和 src 是相同的文件）。</span>

```python
shutil.move(src, dst, copy_function=copy2)

shutil.move('./move.py','../glob_demo')
```

## shutil.rmtree

<span style="color: red; font-size: 22px;">递归地删除目录树。ignore_errors 允许忽略删除过程中出现的错误（例如，如果某些文件或目录由于权限问题而无法删除）。</span>

```python
shutil.rmtree(path, ignore_errors=False, onerror=None)：
```

## shutil.make_archive

<span style="color: red; font-size: 22px;">创建一个归档文件（如 zip、tar 等），其中可以包含多个文件和目录。base_name 是归档文件的名称（不包括扩展名），format 指定归档格式（如 'zip', 'tar', 'gztar', 'bztar', 'xztar'），root_dir 是归档中所有文件和目录的根目录（默认为当前目录）。</span>

```python
shutil.make_archive(base_name, format, root_dir=None, base_dir=None, verbose=0, dry_run=0, owner=None, group=None, logger=None)：
```

<span style="color: blue; font-size: 22px;">shutil 库通过提供这些函数，使得文件和目录的管理变得更加简单和高效。它特别适用于需要批量处理文件或目录的场景，如备份、同步或清理文件系统等任务。</span>

