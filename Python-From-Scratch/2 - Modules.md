# Modules

## What Are Modules in Python?

In Python, you have the ability to import modules, which contain code that other people have written. These modules can add new functionality to python, or make your existing code much smaller.

## How do I use them?

You can use modules by using
```python
import <module>
```

From then on out, you can reference it.

Example:

```python
import time

# Spacing between imports and the actual code for readability

print("Started!")

time.sleep(1) # This is how you delay in python.

print("Delayed!")
```

In addition to `import <module>`, you can also reference them in additional ways.

```python
import time # From above
import time as t # Allows you to shorten it.
from time import sleep # Allows you to reference the sleep() function without putting the "time." at the start
from time import * # imports everything from time into the codebase
```

## Minescript Module

Linking this back to minescript, if you want to interact with minecraft, you have to do it through the `minescript` module.

To reference it, you can import it at the top. I personally prefer to import it below as
```python
from minescript import *
```
because you can then passively discover new minescript functions by typing.

:star: IDE not autocompleting? Visit [here](https://sam-ple.github.io/minescript-sample/docs/FAQ.html#%EF%B8%8F-how-can-i-enable-autocomplete-in-vs-code).

Here is an example where you can print your Minecrat health into chat like before.

```python
from minescript import *

print(player_health())
```
 There are many more uses to minescript that will be shown later!
 
## Community-made modules

Many community-made libraries can be used in minescript. The best location to find more libraries/scripts is the official community [Discord](https://discord.gg/NjcyvrHTze).

When using these modules, simply place them in the same folder that you place your scripts in and they will be available to you.
