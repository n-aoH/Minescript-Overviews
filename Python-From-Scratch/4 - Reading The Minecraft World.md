# Reading The Minecraft World

You're probably very excited to make your scripts interact with the world. An easy stepping point into this is seeing what's directly around the player.

## getblock()

The `getblock()` function will return a string representing what block is at said position. In order to do this however, we first need to find the coordinates to scan.

A good place to start would probably be beneath your feet.

In order to get the player position, there are two equally valid ways to get it:
```python
player_position()
```
and
```python
player().position
```

Each of these will return the same position, it's just up to your preference.

if you decide to print your position:
`print(player_position())`

you'll probably get a crazy number with a lot of decimal places:
`[1351.4567765635304, 63.0, -992.6298281327541]`

What you've just printed is a list, containing the raw X, Y, Z values of the player.

### Using It

In order to actually use this, though, we need to first align it to the coordinate grid of minecraft.

Minecraft floors coordinates to get the `block position` of each mob. (shown below)

<img width="567" height="566" alt="image" src="https://github.com/user-attachments/assets/7909eb1c-23a7-43c8-9d35-b17c37e7f4f2" />

In order to turn the player position into a block position, we can use the `math.floor` function.

```python
from minescript import *
import math

pos = player_position()
x = math.floor(pos[0]) # 1st Item
y = math.floor(pos[1]) # 2nd Item
z = math.floor(pos[2]) # 3rd Item

print(x, y, z)
```

Now we're getting somewhere!

We can substitute the `print(x, y, z)` statement to a getblock() statement to start on our script.

```python
block = getblock(x, y, z) 
print(block)
```

What you probably see is `minecraft:air`.

This makes sense though, because the entity position is located at your feet, meaning we're now getting the block above the one we're standing on.

To fix this, we can simply subtract 1 from y.

```python
y = y -1
# OR
y -= 1
```

## Using getblock() in a script

magma is hot, so we probably want to jump whenever we touch it, right? Let's make a script to do that, combining code from previous modules.

First off, in order to tell if you're standing on magma, we'll do a string comparison. Since the name of a magma block is `minecraft:magma_block`, we can just check if the block we've scanned for contains the word magma.
```python
if "magma" in block:
  print("ouchie!")
```

From here, I challenge you to modify this script to jump one time whenever it detects magma. If you get stuck, you can check the next section.

## Jumping

A piece of code to jump is as follows:

```python
from minescript import *
import math


pos = player_position()
x = math.floor(pos[0])
y = math.floor(pos[1])
z = math.floor(pos[2])

y -= 1
block = getblock(x,y,z)
if "magma" in block:
    player_press_jump(True)
    player_press_jump(False)
```

But when you use this, it only jumps one time. To make it scan continuously, you can use a `while True` loop. Everything inside of the indentation of a while loop will happen forever.

```python
from minescript import *
import math



while True:
    pos = player_position()
    x = math.floor(pos[0])
    y = math.floor(pos[1])
    z = math.floor(pos[2])

    y -= 1
    block = getblock(x,y,z)
    if "magma" in block:
        player_press_jump(True)
        player_press_jump(False)
```

Now you've created a macro that jumps whenever the floor is lava!

You can use these conditional statements inside your future macros to make them more interactive. In future lessons, I'll cover entities, chat listeners, and more ways to make your scripts interact with the minecraft world!
