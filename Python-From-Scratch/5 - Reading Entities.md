# Reading Entities

## entities()

The way you can get the list of all entities that are in render distance is with the entities() function in minescript. 
This returns a list of `entity` objects.
You can then use a `for` loop to iterate through them.

```python
from minescript import *

for entity in entities():
  print(entity.name)
```

We can do a lot more than just printing out names, though!

## Finding nearest entity

To find the nearest entity, we can use the `sort` parameter in the entity() function.

```python
for entity in entities(sort="nearest"):
  print(entity.name)
```

As an example, let's make a script that automatically looks at the nearest entity.
We can read the position using `entity.position`, and look at a set of coordinates using `player_look_at()`.

```python
for entity in entities(sort="nearest"):
  player_look_at(*entity.position) # Star here to expand out the X, Y, Z list into individul arguments
```

But this script chooses to look at every entity. Instead, we want to **only** look at the nearest one. 
Luckily, the `break` command in python can stop a loop early.

```python
for entity in entities(sort="nearest"):
  player_look_at(*entity.position)
  break
```

Hmm. Instead of looking at anything in particular, it seems to break.
The reason why is that the nearest entity to your player is.. well.. your player.
We can exclude this in several ways, but I'll just skip the first entity in the list.

```python

plr = True

for entity in entities(sort="nearest"):
  if plr:
    plr = False
  else:
    player_look_at(*entity.position)
    break
```

## Selective tracking

Now we're actually looking at the nearest entity!
But what if we only want to look for specific entity types?
Here's where we can use the entity's `type` data to our advantage. Only look at it if it also matches our type!

```python
  else:
    if "cow" in entity.type:
      player_look_at(*entity.position)
      break
```

Lastly, like before, you can nestle everything into a `while True` statement in order to make it run repeatedly for tracking.
Reminder: `killjob -1` stops all running scripts.
