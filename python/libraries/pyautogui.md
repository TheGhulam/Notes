## Mouse Control
```python
import pyautogui

pyautogui.size() # Returns res of screen

pyautogui.position() # Get current mouse location

pyautogui.moveTo(10, 10, duration=<secs>) # Move mouse to given co-ords

pyautogui.moveRel(20, 0, duration=<secs>) # Move mouse around 
pyautogui.dragRel(20, 0, duration=<secs>) # Move while clicking

pyautogui.click(10, 10) # Click given coords

pyautogui.doubleClick()
pyautogui.rightClick()
pyautogui.middleClick()

ctypes.windll.user32.SetCursorPos(2200, 700) works
pyautogui.moveTo(2200, 700) doesn't work

```

## Call mouse location function from command line
```python
python
import pyautogui
pyauogui.displayMousePosition()
```

## Keyboard Control
```python

import pyautogui
pyautogui.typewrite('Hello world!', interval=0.2)

pyautogui.typewrite(['a', 'b', 'left', 'left', 'X'], interval=0.2)

# Check keys
pyautogui.KEYBOARD_KEYS

pyautogui.press(<single_key>)

pyautogui.hotkey('ctrl', 'o')
```

## Take screenshots and find co-ords of the image
```python

import pyautogui
pyautogui.typewrite('Hello world!', interval=0.2)

pyautogui.typewrite(['a', 'b', 'left', 'left', 'X'], interval=0.2)

# Check keys
pyautogui.KEYBOARD_KEYS

pyautogui.press(<single_key>)

pyautogui.hotkey('ctrl', 'o')
```
