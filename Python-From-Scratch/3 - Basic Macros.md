# Basic Macros

## Accessing Player Input

The `minescript` module allows you to access player input by using methods such as minescript.player_press_forward()

:star: Side note: You see how these methods we use always have a parentheses `()` at the end? That signifies that they're a method that needs to be executed. Any arguments can be placed inside of the parentheses to pass them through.

When using player input, you get the option to start or end an input, based on the `True` or `False` that you pass into minescript.

```python
import time
from minescript import *


player_press_forward(True)
print("Started walking!")

time.sleep(5)

player_press_forward(False)
print("Stopped walking!")
```

In addition to all of the options shown, you can also use `press_key_bind(name, bool)` to access any keybind in minecraft. The full list gets printed when you make an error, and also includes modded keybinds. 

As an example, using this, we can select the hotbar slot.

```python
press_key_bind("key.hotbar.1", True)

press_key_bind("key.hotbar.1", False) #This is needed to release the key. If you don't do that, you will be stuck on that slot.
```

## Using Minescript vs External Libraries

Using Minescript is always preferable to using external libraries for one main reason: You can still have your scripts running while your minecraft window is out of focus.

If you want to use something like `pyautogui`, you will not be able to use your computer at all while the macro is active. In comparison, using minescript only takes control of your minecraft window.

## Turning

In order to turn you player, you can use player_set_orientation(yaw, pitch).

To turn, you simply add a number to your current pitch.

```python
from minescript import *

yaw = player().yaw
pitch = player().pitch

player_set_orientation(yaw + 45, pitch) # Turn 45 degrees.
```

I have explained minecraft rotation in more detail [here](https://github.com/n-aoH/Minescript-Overviews/blob/main/general/rotation/README.md).


## Defining functions

When you create your scripts, you will often create code snippets that you have to re-use.

Functions can be defined and referenced as follows:
```python
def greet():
  print("Hello!")

greet()

sleep(1)

greet()
```

In addition, you can also pass through arguments. Let's say you want to create a function to move for a specified number of seconds and then stop, in order to execute your next command.

```python
def walk(seconds):
  player_press_forward(True)

  time.sleep(seconds)

  player_press_forward(False)

walk(1)
time.sleep(1)
walk(2)
```

We can also do the same with turning to create a re-usable turn function.

```python

def turn(x, y):
  yaw = player().yaw
  pitch = player().pitch

  player_set_orientation(yaw + x, pitch + y)
```

Putting this all together we can create a simple macro to walk around, referenced similar to:

```python
walk(1)
turn(90,0)
walk(2)
turn(180,0)
walk(1)
```

Congratulations! You've now created a primitive macro! Later lessons will teach you more in order to make it interactive.

# ❗ Important Note

This code is very easy to detect as a macro.

If you are planning on using it on a server, use a community-made tweening library to make your turns more gradual and less snappy.

You can also create one yourself if you're advanced enough.
