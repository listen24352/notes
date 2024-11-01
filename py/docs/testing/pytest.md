[TOC]

# pytest

## 安装版本查询

```python
pip install pytest

(.venv) leo@foucs:~/Desktop$ pytest -v
============================================================== test session starts ===============================================================
platform linux -- Python 3.10.12, pytest-8.3.3, pluggy-1.5.0 -- /home/leo/Desktop/demo/.venv/bin/python
cachedir: .pytest_cache
rootdir: /home/leo/Desktop
collected 0 items                                                                                                                                

============================================================= no tests ran in 0.07s ==============================================================
```

## pytest命令行

```python
usage: pytest [options] [file_or_dir] [file_or_dir] [...]
# 运行
pytest

# 简洁模式 
pytest -q test_*.py

# -k
只运行与给定子字符串表达式匹配的测试。表达式就是Python可求值表达式，其中所有名称都与测试名称及其子字符串匹配父类。
示例：
-k ‘test_method or test_other’匹配所有测试函数和类名中包含‘test_method’或‘test_other’，
-k ‘not test_method’匹配那些名字中不包含‘test_method’的。
-k 'not test_method and Not test_other'将消除匹配。此外，关键字与类匹配
以及在‘extra_keyword_matches’集合中包含额外名称的函数，以及函数的名称直接分配给它们。匹配不区分大小写。
```

# pytest核心功能

## 如何调用pytest

### 指定要运行的测试

```python
# 1.在模块中运行测试
pytest test_mod.py


# 2.在目录中运行测试
pytest testing/


# 3.按关键字表达式运行测试
pytest -k 'MyClass and not method'


# 4.按集合参数运行测试

# 在模块中运行特定测试
pytest tests/test_mod.py::test_func

# 运行类中的所有测试
pytest tests/test_mod.py::TestClass

# 指定特定的测试方法
pytest tests/test_mod.py::TestClass::test_method

# 指定测试的特定参数化
pytest tests/test_mod.py::test_func[x1,y2]

# 4.按标记表达式运行测试

# 运行所有使用 @pytest.mark.slow 装饰器装饰的测试
pytest -m slow

# 要运行所有使用带注释的 @pytest.mark.slow（phase=1） 装饰器装饰的测试，并将 phase 关键字参数设置为 1：
pytest -m "slow(phase=1)"

# 5.从包运行测试
pytest --pyargs pkg.testing

# 6.从文件中读取参数
pytest @tests_to_run.txt

# tests_to_run.txt 内容
tests/test_file.py
tests/test_mod.py::test_func[x1,y2]
tests/test_mod.py::TestClass
-m slow
# 可以用pytest --collect-only -q 生成

```

### 获取有关版本、选项名称、环境变量的帮助

```python
(tests) leo@foucs:~/important/study_git/tests$ pytest --version
pytest 8.3.3
```

```python
(tests) leo@foucs:~/important/study_git/tests$ pytest --fixtures
============================================= test session starts ==============================================
platform linux -- Python 3.10.12, pytest-8.3.3, pluggy-1.5.0
rootdir: /home/leo/important/study_git/tests
plugins: trio-0.8.0
collected 8 items                                                                                              
cache -- .../_pytest/cacheprovider.py:556
    Return a cache object that can persist state between testing sessions.

capsysbinary -- .../_pytest/capture.py:1006
    Enable bytes capturing of writes to ``sys.stdout`` and ``sys.stderr``.

capfd -- .../_pytest/capture.py:1034
    Enable text capturing of writes to file descriptors ``1`` and ``2``.

capfdbinary -- .../_pytest/capture.py:1062
    Enable bytes capturing of writes to file descriptors ``1`` and ``2``.

capsys -- .../_pytest/capture.py:978
    Enable text capturing of writes to ``sys.stdout`` and ``sys.stderr``.

doctest_namespace [session scope] -- .../_pytest/doctest.py:741
    Fixture that returns a :py:class:`dict` that will be injected into the
    namespace of doctests.

pytestconfig [session scope] -- .../_pytest/fixtures.py:1345
    Session-scoped fixture that returns the session's :class:`pytest.Config`
    object.

record_property -- .../_pytest/junitxml.py:280
    Add extra properties to the calling test.

record_xml_attribute -- .../_pytest/junitxml.py:303
    Add extra xml attributes to the tag for the calling test.

record_testsuite_property [session scope] -- .../_pytest/junitxml.py:341
    Record a new ``<property>`` tag as child of the root ``<testsuite>``.

tmpdir_factory [session scope] -- .../_pytest/legacypath.py:298
    Return a :class:`pytest.TempdirFactory` instance for the test session.

tmpdir -- .../_pytest/legacypath.py:305
    Return a temporary directory path object which is unique to each test
    function invocation, created as a sub directory of the base temporary
    directory.

caplog -- .../_pytest/logging.py:598
    Access and control log capturing.

monkeypatch -- .../_pytest/monkeypatch.py:31
    A convenient fixture for monkey-patching.

recwarn -- .../_pytest/recwarn.py:35
    Return a :class:`WarningsRecorder` instance that records all warnings emitted by test functions.

tmp_path_factory [session scope] -- .../_pytest/tmpdir.py:242
    Return a :class:`pytest.TempPathFactory` instance for the test session.

tmp_path -- .../_pytest/tmpdir.py:257
    Return a temporary directory path object which is unique to each test
    function invocation, created as a sub directory of the base temporary
    directory.


----------------------------------- fixtures defined from pytest_trio.plugin -----------------------------------
mock_clock -- ../../../.venv/tests/lib/python3.10/site-packages/pytest_trio/plugin.py:552
    no docstring available

autojump_clock -- ../../../.venv/tests/lib/python3.10/site-packages/pytest_trio/plugin.py:557
    no docstring available

nursery -- ../../../.venv/tests/lib/python3.10/site-packages/pytest_trio/plugin.py:562
    no docstring available


============================================ no tests ran in 0.02s =============================================
```

```python

(tests) leo@foucs:~/important/study_git/tests$ pytest -h | help
GNU bash，版本 5.1.16(1)-release (x86_64-pc-linux-gnu)
这些 shell 命令是内部定义的。输入 "help" 以获取本列表。
输入 "help 名称" 以得到有关函数 "名称" 的更多信息。
使用 "info bash" 来获得关于 shell 的更多一般性信息。
使用 "man -k" 或 "info" 来获取不在本列表中的命令的更多信息。

名称旁边的星号 (*) 表示该命令被禁用。

 任务说明符 [&]                                          history [-c] [-d 偏移量] [n] 或 history -anrw [文件>
 (( 表达式 ))                                            if 命令; then 命令; [ elif 命令; then 命令; ]... [ e>
 . 文件名 [参数]                                         jobs [-lnprs] [任务说明符 ...] 或 jobs -x 命令 [参>
 :                                                       kill [-s 信号说明符 | -n 信号编号 | -信号说明符] pid>
 [ 参数... ]                                             let 参数 [参数 ...]
 [[ 表达式 ]]                                            local [选项] 名称[=值] ...
 alias [-p] [名称[=值] ... ]                             logout [n]
 bg [任务说明符 ...]                                     mapfile [-d 分隔符] [-n 计数] [-O 起始] [-s 计数] [->
 bind [-lpvsPSVX] [-m 键映射] [-f 文件名] [-q 名称] [->  popd [-n] [+N | -N]
 break [n]                                               printf [-v var] 格式 [参数]
 builtin [shell-内建 [参数 ...]]                         pushd [-n] [+N | -N | 目录]
 caller [表达式]                                         pwd [-LP]
 case 词语 in [模式 [| 模式]...) 命令 ;;]... esac        read [-ers] [-a 数组] [-d 分隔符] [-i 文本] [-n 字>
 cd [-L|[-P [-e]] [-@]] [目录]                           readarray [-d 分隔符] [-n 计数] [-O 起始] [-s 计数] >
 command [-pVv] 命令 [参数 ...]                          readonly [-aAf] [名称[=值] ...] 或 readonly -p
 compgen [-abcdefgjksuv] [-o 选项] [-A 动作] [-G 全局>  return [n]
 complete [-abcdefgjksuv] [-pr] [-DEI] [-o 选项] [-A >  select 名称 [in 词语 ... ;] do 命令; done
 compopt [-o|+o 选项] [-DEI] [名称 ...]                  set [--abefhkmnptuvxBCHP] [-o 选项名] [--] [参数 ..>
 continue [n]                                            shift [n]
 coproc [名称] 命令 [重定向]                             shopt [-pqsu] [-o] [选项名 ...]
 declare [-aAfFgiIlnrtux] [-p] [name[=value] ...]        source 文件名 [参数]
 dirs [-clpv] [+N] [-N]                                  suspend [-f]
 disown [-h] [-ar] [任务说明符 ... | pid ...]            test [表达式]
 echo [-neE] [参数 ...]                                  time [-p] 流水线
 enable [-a] [-dnps] [-f 文件名] [名称 ...]              times
 eval [参数 ...]                                         trap [-lp] [[参数] 信号说明符 ...]
 exec [-cl] [-a 名称] [命令 [参数 ...]] [重定向 ...]     true
 exit [n]                                                type [-afptP] 名称 [名称 ...]
 export [-fn] [名称[=值] ...] 或 export -p               typeset [-aAfFgiIlnrtux] [-p] name[=value] ...
 false                                                   ulimit [-SHabcdefiklmnpqrstuvxPT] [限制]
 fc [-e 编辑器名] [-lnr] [起始] [终止] 或 fc -s [模式>   umask [-p] [-S] [模式]
 fg [任务说明符]                                         unalias [-a] 名称 [名称 ...]
 for 名称 [in 词语 ... ] ; do 命令; done                 unset [-f] [-v] [-n] [名称 ...]
 for (( 表达式1; 表达式2; 表达式3 )); do 命令; done      until 命令; do 命令; done
 function 名称 { 命令 ; } 或 name () { 命令 ; }          variables - 一些 shell 变量的名称和含义
 getopts 选项字符串 名称 [参数 ...]                      wait [-fn] [-p 变量] [id ...]
 hash [-lr] [-p 路径名] [-dt] [名称 ...]                 while 命令; do 命令; done
 help [-dms] [模式 ...]                                  { 命令 ; }
(tests) leo@foucs:~/important/study_git/tests$ 

```

### 分析测试执行持续时间

```python
# 要获取持续时间超过 1.0 秒的最慢的 10 个测试持续时间的列表，请执行以下操作：
pytest --durations=10 --durations-min=1.0
```

### 管理插件的加载

```python
# 加载插件
pytest -p mypluginmodule
pytest -p pytest_cov

# 禁用插件
pytest -p no:doctest
```

### 调用 pytest 的其他方式

```python
# content of myinvoke.py
import sys

import pytest


class MyPlugin:
    def pytest_sessionfinish(self):
        print("*** test run reporting finishing")


if __name__ == "__main__":
    sys.exit(pytest.main(["-qq"], plugins=[MyPlugin()]))
```



## 如何在测试中编写和报告断言

## 如何使用 Fixtures

## 如何使用属性标记测试函数

## 如何参数化 fixture 和测试函数

## 如何在测试中使用临时目录和文件

## 如何 monkeypatch/mock 模块和环境

## 如何运行 doctests

## 如何重新运行失败的测试并在测试运行之间保持状态
