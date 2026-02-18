# Fishing guide

This guide will go over the basics of making a fishing script inside of minescript.

## Getting Started

First off, let's figure out the individual problems to solve when making this script.

When fishing, I identify the following steps:

1. Find the bobber entity
2. Figure out when the fish bites
3. Reeling and Casting
4. Polish

## 1. Finding the bobber

To start, we need to figure out.. which bobber is ours.

We could check every entity every time and then read the bites from there, but that approach would break if someone else were to fish anywhere near us.

```python
def find_bobber(): #Find it occasionally
  for entity in entities(sort="nearest",max_distance=3):
```

Here we check the nearest first, so that we can simply use a `return` once we find the bobber to instantly leave it, saving time.

Additionally, whenever we are looking for the bobber, we know that it's going to start somewhere near us. A max distance of 3 is fairly liberal and ensures that whenever our bobber spawns, we will garunteed identify it. *this can be changed later if you get false positives.*

Because we have this value set low to start with, start your tests with the rod reeled in before you start fishing.

```python
def find_bobber():
  for entity in entities(sort="nearest",max_distance=3):

    if "bobber" in entity.type: #Identify it
      return entity.uuid #This is the nearest bobber

  # After the loop
  return false # No bobber found
```


Now, we can use this function to identify if we have our line out, as well as the properties of our bobber.

Below `find_bobber`, we can create a loop to start reading data from it.

**⭐ Tip:** Use `\killjob -1` to clear out all scripts if you have an infinite script running. 

```python
bobber = find_bobber() #check if it's already out

while True:

    bobber_found = False #Start off by storing if we've found it


    for entity in entities():
        if entity.uuid == bobber: #Check for our bobber in the entities


            print(entity.velocity) # Print out velocity
            bobber_found = True # Yay! we found the bobber!
    
    if not bobber_found: #If we don't have our bobber's UUID in the entity, list, it has disappeared.
        bobber = find_bobber() #Check again to see if we can find it.
```

## 2. Figure out when the fish bites

If you play around with the script, you'll see that every time a fish bites, the velocity spikes down as it dips below the surface.

`entity.velocity` returns a list of \[X, Y, Z\] velocities.

We can simply read the Y velocity of the bobber, we can find out if we should reel!

```python
if entity.velocity[1] < -.2:
  reel()
```

*However,* there is a new edge case. if the bobber is hooked onto an entity or still getting flung out, it will also trigger this simple check.

To fix it, we can make sure that the X and Z velocities are relatively small.

We use absolute value here because an X velocity value of -.2 would still be considered "less than .1".

```python
if entity.velocity[1] < -.2:
  if abs(entity.velocity[0]) < .1 and abs(entity.velocity[2]) < .1:
    print("reel")
```

Let's add this into our script in place of the print statement.

```python


    for entity in entities():
        if entity.uuid == bobber: #Check for our bobber in the entities

            if entity.velocity[1] < -.2: #Check for y velocity first
              if abs(entity.velocity[0]) < .1 and abs(entity.velocity[2]) < .1: #Check for X and Z velocity second

                print("reel")  # Coming soon™
            
            bobber_found = True # Yay! we found the bobber!
```

Crucially we keep the `bobber_found` outside of the check as we still want to keep the UUID cached.

Now, you can run it to see when the script thinks it should pull the rod!

## 3. Reeling it in

What we need to do from here to reel it in is to right click twice. (once to reel in, another to cast out)

Because we need to wait in between actions, the `time` module from python is needed from here.

```python
def reel():
  player_press_use(True) #reel in
  player_press_use(False)

  time.sleep(.3)

  player_press_use(True) #cast out
  player_press_use(False)
```

We use press use `True` to set to begin right clicking, but then we have to press use `False` to stop right clicking.

Now, we can substitute in the `reel()` function into the place of the print statement.

```python
            if entity.velocity[1] < -.2:
                if abs(entity.velocity[0]) < .1 and abs(entity.velocity[2]) < .1:
                    reel() # addition here
```

Now, we have the basic outline of a fishing script!

## 4. Polish

From here, there's more you can do, particularly to humanize it.

I will not go over how to do them here, consider them programming challenges to implement on your own.

1. Add random delays

Using `random.uniform()`, you can make more human-like delays, and simulate reaction time.

2. Move the camera slightly

Pick either your favorite camera smootherning library or the `minescript.set_player_orientation(yaw, pitch)` function to set the player orientation, again, with random offsets.

Hint: You can read the player's pitch and yaw by using `player().pitch` and `player().yaw`

3. Play fishing minigames

There are a variety of other server plugins that add more reaction-based mechanics to fishing.

The community-made library `minescript_plus` has more tools to help you out, including reading announcement text used in some fishing plugins!

## Bare-bones script

Here's the final script to check your understanding by.

```python
from minescript import *
import time

def find_bobber():
    for entity in get_entities(sort="nearest",max_distance=3):
        if "bobber" in entity.type:
            return entity.uuid
    
    return False

def reel():
  player_press_use(True) 
  player_press_use(False)

  time.sleep(.3)

  player_press_use(True) 
  player_press_use(False)

bobber = find_bobber()

while True:

    bobber_found = False

    for entity in entities():
        if entity.uuid == bobber:

            if entity.velocity[1] < -.2:
                if abs(entity.velocity[0]) < .1 and abs(entity.velocity[2]) < .1:
                    reel()


            bobber_found = True
    
    if not bobber_found:
        bobber = find_bobber()
```

Good luck on your minescripting journey! If you're ever having trouble, you can reach out for help on the official discord server.
