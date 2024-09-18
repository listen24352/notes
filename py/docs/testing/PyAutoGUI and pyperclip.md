# PyAutoGUI

> PyAutoGUI是一个纯Python编写的GUI自动化库，它可以模拟鼠标和键盘操作，如移动鼠标、点击鼠标、滚动鼠标滚轮、输入文本等。以下是PyAutoGUI库中常用的一些方法：

```python
pip install pyautogui
import time  

pyautogui.moveTo(800, 556, duration=0.1)
# pyautogui.click(800, 556, button='left')  # 单击左键
pyautogui.doubleClick(800, 556)


# 1. 获取屏幕和鼠标信息
获取鼠标当前位置：pyautogui.position()，返回鼠标当前的X和Y坐标。
获取屏幕尺寸：pyautogui.size()，返回屏幕的宽度和高度（以像素为单位）。
判断坐标是否在屏幕上：pyautogui.onScreen(x, y)，传入X和Y坐标，如果坐标在屏幕内则返回True，否则返回False。

# 2. 鼠标操作
移动鼠标：
pyautogui.moveTo(x, y, duration=seconds)：在指定时间内将鼠标移动到屏幕的(x, y)位置。
pyautogui.moveRel(xOffset, yOffset, duration=seconds)：根据当前鼠标位置，向指定方向移动指定的像素距离。

点击鼠标：
pyautogui.click(x=moveToX, y=moveToY, button='left', clicks=1, interval=0.0)：在指定位置点击鼠标，可以设置点击次数和间隔时间。

pyautogui.doubleClick(x=moveToX, y=moveToY, button='left', interval=0.0)：在指定位置双击鼠标。

pyautogui.rightClick(x=moveToX, y=moveToY)、pyautogui.middleClick(x=moveToX, y=moveToY)：在指定位置执行右键或中键点击。

鼠标拖拽：
pyautogui.dragTo(x, y, duration=seconds, button='left')：将鼠标拖动到指定位置。
pyautogui.dragRel(xOffset, yOffset, duration=seconds, button='left')：从当前位置开始，向指定方向拖动鼠标。

鼠标滚轮滚动：pyautogui.scroll(clicks, x=None, y=None)，向上或向下滚动鼠标滚轮，clicks为正数时向上滚动，为负数时向下滚动。

  
# 确保pyautogui有足够的时间来响应  
time.sleep(2)  # 等待2秒，给你时间切换到目标窗口  
  
# 向上滚动5次  
pyautogui.scroll(5)  
print("鼠标滚轮向上滚动了5次")  
  
# 等待一点时间，以便你可以看到效果  
time.sleep(1)  
  
# 向下滚动3次，这次我们在屏幕上的特定位置执行（例如，屏幕中央）  
screen_width, screen_height = pyautogui.size()  # 获取屏幕尺寸  
x = screen_width // 2  # 屏幕宽度的一半  
y = screen_height // 2  # 屏幕高度的一半  
pyautogui.scroll(-3, x=x, y=y)  
print("在屏幕中央，鼠标滚轮向下滚动了3次")  
  
# 注意：在实际应用中，可能需要调整time.sleep()的等待时间，以确保pyautogui的操作有足够的时间来执行和响应。  
# 此外，确保你的目标窗口在pyautogui执行操作时是活动状态。


# 3. 键盘操作
按键操作：
pyautogui.press(keys, presses=1, interval=0.0)：模拟按键操作，可以模拟单个按键或多个按键（列表形式）。
pyautogui.keyDown(key)和pyautogui.keyUp(key)：分别模拟按下和释放指定按键。
pyautogui.hotkey(*keys)：模拟组合键操作，如pyautogui.hotkey('ctrl', 'c')模拟Ctrl+C。
输入文本：pyautogui.typewrite(message, interval=0.0)，在键盘光标处输入文本，可以设置字符间的间隔时间。

# 4. 屏幕操作
截屏：pyautogui.screenshot()可以捕获当前屏幕的截图，并返回一个Pillow图像对象。还可以将其保存到文件，如pyautogui.screenshot('screenshot.png')。
图像识别：通过pyautogui.locateOnScreen('image.png')可以在屏幕上查找指定图像的位置，返回图像左上角坐标的元组。

# 5. 其他功能
故障保险：通过pyautogui.FAILSAFE = True启用故障安全模式，当鼠标移动到屏幕左上角时，程序将抛出FailSafeException异常以中断运行。
停顿：pyautogui.PAUSE可以设置每次操作后的暂停时间（以秒为单位），但更推荐使用time.sleep()进行精确控制。
```

# pyperclip

> 1.用于复制剪贴板里的内容、
>
> 2.向剪贴板写入内容。

```python
pip install pyperclip

# # 将图片文件复制到剪贴板上
pyperclip.copy(r'C:\Users\Admin\Desktop\UIAutomation\test.docx')  
pyperclip.paste()  # 获取剪贴板上的内容
pyautogui.hotkey('ctrl', 'v')  # 将剪贴板上的文件路径粘贴到应用窗口
pyautogui.press('enter')  # 模拟回车
```



