# First Pyjinn File

This guide will go through creating your first Pyjinn file.

First, go to your `minescript` folder and add a new file.

Instead of it being called `<FILENAME>.py`, it will instead be `<FILENAME>.pyj`. 

:star: The .pyj extension tells minescript to execute it as a Pyjinn file instead of a Python file.

Whenever you open this file in your IDE, it will not know what to do with it, as .pyj is not a standard filetype.

You can either:

1. (temporary solution) Add `#!python` to the top of the script

2. (permanent solution) Go to settings (`Ctrl+,`) → `files:associations` and add `**/*.pyj` with a value of `python`

This will tell your IDE that a .pyj file is actually a python file, and to check it as such.
