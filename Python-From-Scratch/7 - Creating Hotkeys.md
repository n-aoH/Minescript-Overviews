# Creating Hotkeys

It's annoying to have to type in `\SCRIPT NAME` in chat every time you want something to happen, so this guide will go over setting up a hotkey-based system to activate your macros.

Uses info from the official [Minescript Docs](https://minescript.net/docs).

## Finding your reference key

Minescript uses minecraft's GLFW keycode API to reference keys, so you have to reference them from a list.

The full list of keycodes is available [here](https://minescript.net/docs).

To reference a key in minescript, navigate to the number of the key you want to use.

```py
KEY_MACRO = 264 #GLFW key 264 is down arrow
```

## Using the key in the Event Queue

Key events, can pass through parameters similar to other events. Here's a brief listing of the ones you care about.

```py
key: int #GLFW keycode
action: int # 0: button down | 1: button up | 2: button held
screen: str # The screen used. Helps if you want to only take inputs outside of GUIS. (if event.screen != null)
```

```py

with EventQueue() as event_queue:
  event_queue.register_key_listener()
  while True:
    #Inside of this loop now is the key events
    event = event_queue.get()
    if event.type == EventType.KEY:
      if event.key == KEY_MACRO and event.action == 1:
        start_macro()
```

Here, setting up `start_macro()` before this block will call that block every time you hit the down arrow key (if it's not already active of course!)

`⭐ Make sure to always define your functions above your main loop.`

However, using this, we still can't take input during the macro loop, only between macros. Depending on your purposes, this may be enough for you.

*The next guide will cover adding multiple event queues and the basics of multiple processes at once. This allows for you to take input while your existing loops are running!*
