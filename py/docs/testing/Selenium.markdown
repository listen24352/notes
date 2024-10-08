[TOC]

# WebDriver

<p style="color: red; font-size: 22px;">
    真正的用户正在操作浏览器
</p>

[examples](https://github.com/SeleniumHQ/seleniumhq.github.io/tree/trunk/examples/python)

## 入门

### 安装

[无网url](https://files.pythonhosted.org/packages/aa/85/fa44f23dd5d5066a72f7c4304cce4b5ff9a6e7fd92431a48b2c63fbf63ec/selenium-4.25.0-py3-none-any.whl)

```python
# 有网首选
pip install selenium

# 无网
下载 .whl 文件（无网url）
pip install *.whl
pip install selenium-4.25.0-py3-none-any.whl
```

### first_selenium.py

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

# 1. 使用驱动实例开启会话
driver = webdriver.Chrome()

# 2. 在浏览器上执行操作
driver.get("https://www.selenium.dev/selenium/web/web-form.html")

# 3. 请求 浏览器信息
title = driver.title
print(title)

# 4. 建立等待策略
driver.implicitly_wait(0.5)

# 5. 发送命令 查找元素
text_box = driver.find_element(by=By.NAME, value="my-text")
submit_button = driver.find_element(by=By.CSS_SELECTOR, value="button")

# 6. 操作元素
text_box.send_keys("Selenium")
submit_button.click()

# 7. 获取元素信息
message = driver.find_element(by=By.ID, value="message")
text = message.text
print(text)

# 8. 结束会话
# 这将结束驱动程序进程, 默认情况下, 该进程也会关闭浏览器. 无法向此驱动程序实例发送更多命令.
driver.quit()
```

[使用selenium](https://www.selenium.dev/zh-cn/documentation/webdriver/getting_started/using_selenium/)

> Web 应用的自动化测试、重复性任务、网页爬虫
>
> Test Runner
> 即使不使用 Selenium 做测试，如果你有高级用例，使用一个 test runner 去更好地组织你的代码是很有意义的。学会使用 before/after hooks 和分组执行或者并行执行将会非常有用。
>
> pytest - 由于其简单性和强大的插件，许多人的首选。

```python
from selenium import webdriver
from selenium.webdriver.common.by import By


def test_eight_components():
    driver = setup()

    title = driver.title
    assert title == "Web form"

    driver.implicitly_wait(0.5)

    text_box = driver.find_element(by=By.NAME, value="my-text")
    submit_button = driver.find_element(by=By.CSS_SELECTOR, value="button")

    text_box.send_keys("Selenium")
    submit_button.click()

    message = driver.find_element(by=By.ID, value="message")
    value = message.text
    assert value == "Received!"

    teardown(driver)

def setup():
    driver = webdriver.Chrome()
    driver.get("https://www.selenium.dev/selenium/web/web-form.html")
    return driver

def teardown(driver):
    driver.quit()

```

## 驱动

[远程驱动](https://www.selenium.dev/zh-cn/documentation/webdriver/drivers/remote_webdriver/)

### 选项

```python
options = webdriver.ChromeOptions()
```

### 服务

```python
# 默认服务
service = webdriver.ChromeService()
driver = webdriver.Chrome(service=service)

# 驱动位置 
service = webdriver.ChromeService(executable_path=chromedriver_bin)

# 驱动程序端口
service = webdriver.ChromeService(port=1234)
```

## 浏览器

### Chrome特定功能

> 默认情况下，Selenium 4与Chrome v75及更高版本兼容. 但是请注意Chrome浏览器的版本与chromedriver的主版本需要匹配.

[chrome](https://www.selenium.dev/zh-cn/documentation/webdriver/browsers/chrome/#service)

```python

```



## 等待

### 隐式

```python

```

### 显示

```python

```

### 强制

```

```

## 元素

## CDP

## 交互

## Actions接口

## BiDi API

## 额外功能

## 故障排除



# Selenium Manager

<p style="color: red; font-size: 22px;">
    Selenium Manager 是 Selenium 项目的官方驱动程序管理器，它在每个 Selenium 版本中都是开箱即用的。对应浏览器包含版本<br>
    Chrome：Selenium 4.11.0<br>
    Firefox: Selenium 4.12.0<br>
    Edge： Selenium 4.14.0
</p>

使用 Selenium 驱动 Chrome 的典型示例。假设在启动新会话时，本地计算机上没有安装 Chrome驱动。在这种情况下，Selenium Manager 将发现、下载和缓存当前稳定的 CfT 版本（在 ~/.cache/selenium/chrome 中）。

# Grid

<p style="color: red; font-size: 22px;">
    本地控制测试用例、远端自动执行。<br>
    可以在不同平台的不同机器上运行测试用例。<br>
    多个浏览器和操作系统的组合上运行测试。
</p>



# Selenium IDE

[Selenium IDE是一个记录和回放用户操作的浏览器扩展](https://www.selenium.dev/selenium-ide/docs/en/introduction/getting-started)

## 安装

https://addons.mozilla.org/en-US/firefox/addon/selenium-ide/

### 查看扩展

- Chrome：chrome://extensions
- Firefox： about：addons

## 开始使用

> Record a new test in a new project 在新项目中录制新测试
> Open an existing project 打开现有项目
> Create a new project 创建新项目
> Close the IDE 关闭 IDE







