# Advanced Event Queue

This guide will go over using the built-in `threading` module from python to execute multiple processes at once.

Whenever you combine EventQueues, you have the choice of using multiple listeners on the same queue, or threads to seperate them. 

I personally prefer to use threads, but you can check the `event.type` variable within a queue to figure out which event it came from.

## Why use threads?

As a basic example of why threading is necessary, let's start with our macro from earlier.

``py 
with EventQueue() as event_queue:
  event_queue.register_key_listener()
  while True:
    #Inside of this loop now is the key events
    event = event_queue.get()
    if event.type == EventType.KEY:
      if event.key == KEY_MACRO and event.action == 1:
        start_macro()
```

This will work fine if `start_macro()` is defined as something like
```py
for entity in entities():
  print(entity.name)
  time.sleep(0.2)
```

But what if it were defined as an infinite loop?

```py
while True:
  player_press_jump(True)
  player_press_jump(False)
```

You wouldn't be able to stop it.

But instead, if we seperate the eventQueue() and start_macro() onto different threads, you could easily stop it.

## Creating a thread

Threads are easy to create and run. In the context of:
```py

key_thread()

main_thread()
```

You can monitor and join threads together, but this guide will only go over the one time set-and-forget method of starting a thread.

Let's turn the `start_macro()` function into its own seperate thread, `macro_thread()`.

```py
import threading

toggle = True # Will be used later in the key thread

def macro_thread():
  while True:
    if toggle:
      player_press_jump(True)
      player_press_jump(False)

threading.Thread(target=macro_thread,daemon=True).start()
```

Starting a thread is that easy. Here's what the arguments we're passing do:

```
target - Function for the thread to execute. Do not include the "()" when typing it.
daemon - Determines if a thread is in the "background." If only background threads are present with nothing in the foreground, python will close the script.
.start() - starts the thread. You can create a reference to the thread object, but it's not necessary to start one.
```

With that snippet at the top, you will now always jump whenever toggle is `True` and stop whenever it's `False`.

## Communicating between threads

We don't have to put the eventQueue into its own thread, so for now, I'll just show placing it in main.

After you've created your `macro_thread()`, you can change out the `start_macro()` line.

```py
with EventQueue() as event_queue:
  event_queue.register_key_listener()
  while True:
    #Inside of this loop now is the key events
    event = event_queue.get()
    if event.type == EventType.KEY:
      if event.key == KEY_MACRO and event.action == 1:

        #NEW Addition
        toggle = not toggle # flips it.
```

And now we have a toggle! This method works for any input or thread that you need. 

`⭐ Don't forget to use the global keyword when making a function use a global variable!`
