# Pyjinn From Scratch

This guide assumes that you already know a reasonable amount of python, and covers Pyjinn-specific features.

If you are not already firmiliar with Minescript, I would recommend following Python-From-Scratch before beginning this series.

# Differences From Python

Before we begin, it's important to note what makes Pyjinn scripts different from Python scripts, and the limitations that come from them.

Pyjinn scripts are compiled into java code, but use Python syntax. This means you get a lot of Java features, but no longer get many Python ones.

## Libraries

The difference that you will probably notice first is that Pyjinn scripts do not get access to the entire Python module list.

This means that you lose access to:

```
time module
tkinter module
keyboard module
any other standard python modules
```

However, Pyjinn has limited support for some modules. EX:

```
# tester.py // \tester TESTARG
import sys

print(sys.argv[1])
```

There is a high likelihood that you will be able to use `math` and `random` in the next release of minescript.
I am currently in the process of implementing some standard Python modules into Pyjinn, but don't expect anything like keyboard or tkinter to come ;)

In exchange for losing all of this, you get access to the [entire standard java library](https://docs.oracle.com/en/java/javase/25/core/java-core-libraries1.html) as well as minecraft's internal javaclasses.

Accessing these has no delay, unlike in Python. This means that if you are doing large amounts of work with minecraft's javaclasses, you should consider putting them into a Pyjinn script, or embedding said script into your python script.

## Sleep()

Currently, Pyjinn scripts lack the ability to use sleep(). There are plans to allow for it later™️, but keep that in mind when designing your scripts.

This is because Pyjinn scripts run on the same thread as your game's rendering, so pausing the script would also pause your rendering and well.. crash.

## Large Loops

Remember how pausing your Pyjinn script will crash your minecraft instance? Performing too many calculations (usually with large loops) will also cause this.

Large operations should be chunked into pieces instead of all being done at once. There are some Pyjinn specific functions like `set_timeout()` and `set_interval()`
that will help you to add delays and pauses into your scripts without crashing.

## Embedded Pyjinn

All these upsides to Pyjinn are great, but what if you wanted to do something that absolutely requires both a Python library (like a tkinter/dpg window) and Pyjinn (Rendering polygons ingame) ?

Luckily, Pyjinn scripts can be embedded into Python scripts to allow you to get the best of both worlds.

```
# tester.py // \tester

import time
from minescript import *
from java import *

print("Hello from Python!")
time.sleep(1)
print("This script can use any Python module!")

time.sleep(1)

pyjinn_script = eval_pyjinn_script(r"""

print("Hello from Pyjinn!")

x = 5

""")

pyj_x = pyjinn_script.get("x")

print("Pyjinn script's X variable: "+pyj_x)
```

Embedding Pyjinn can be overwhelming, but it can also be necessary for some larger projects. For most cases though, you can keep your script in entirely python or entirely pyjinn. 
There's usually workarounds like having your script's GUI be rendered ingame instead of in a separate window.
