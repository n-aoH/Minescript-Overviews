# Reacting To Chat

The event queue in minescript has a lot of overhead code to get started with (referred to as boilerplate). You don't have to completely understand what's going on to get through it, as you will always have access to the minescript documentation to copy and alter to your needs.

It can be overwhelming at first, but gets significantly easier over time. The next few guides will cover the event queue, since it's an extremely important part of minescript that is necessary to make your scripts dynamic. That being said, feel free to skip over guides `6-8` in order to come back to it at a later date.

## Event Queue

There are many events in minescript (keyboard, mouse, chat, entities getting added, block updates, recieving items/damage, explosions, chunks getting loaded, server changes)
that occur sperradically, needing to be accessed by the event queue.

Some boiler plate (from the [minescript documentation](https://minescript.net/docs)) is below:

```python

with EventQueue() as event_queue:
  # Loops in this indentation only actually fire when there's a new event, and are guarunteed to get every event.

  event_queue.register_chat_listener()
  # This tells minescript which events to actually tell your script about (for the while true statement.)

  while True: # Forever
  
    event = event_queue.get()
    # Waits for one event at a time, this is the thing that actually blocks and waits for another one to happen.
    
    if event.type == EventType.CHAT:
    # Filters out the chat type specifically, you can add different checks to have more things using the same event queue.

      if not event.message.startswith("> "):
      # Filters out messages so that they are not repeated infinitely

        echo(f"> Got chat message: {event.message}") # Actual thing to do
```

If you remember, we can also define functions and read the world around us. Combining this together, you can create more elaborate scripts.

```python

with EventQueue() as event_queue:
  event_queue.register_chat_listener()

  while True:

    if event.type == EventType.CHAT:
      if "what is your position?" in event.message.lower():
      #Using the string.lower() function here will make it so that you can type in uppercase or lowercase.

        chat("My position is: "+player().position)
        # If you want, you can round it off, or use blockpos() to automatically convert it.
```

There are many more events in minescript, listed [here](https://minescript.net/docs#eventqueue).
In addition, they also all have unique properties. The event proprties are all listed [here](https://minescript.net/docs#chatevent).

It's a lot to take in, but that's the basics of using the event queue.
There are several more events to look through, but it's not worth your time for me to list out all of them to you.
The minescript documentation has the rest of the boilerplate code for you to insert different events into your programs.

The next guide will cover taking key/mouse input, since there's more work needed for those events specifically.
I'll cover using them to make a keybind, and later how to implement them as a toggle in your scripts.
