# Installing Minescript Plus

## Branches

There are two branches to Minescript Plus. The main branch has been tested the most, and will likely not have changes to its API. For this reason, I recommend downloading it from the `main` branch.

https://github.com/R4z0rX/minescript-scripts/blob/main/Minescript-Plus/minescript_plus.py

Occasionally, you will find more cutting-edge scripts that require the latest Minescript Plus functions. If a script you're using requires this, you can download it from the `beta` branch.

https://github.com/R4z0rX/minescript-scripts/blob/dev/Minescript-Plus/minescript_plus.py

## Downloading

To download Minescript Plus, click the "download raw file" button at the top of the python file.

<img width="1732" height="164" alt="image" src="https://github.com/user-attachments/assets/bc87da4e-e49e-4ae5-894f-56c480ced0d3" />

## Placing it in your Minecraft folder

You've likely created at least one script at this point. You can place Minescript Plus (and any other library files) in the same directory as your other scripts.

<img width="515" height="18" alt="image" src="https://github.com/user-attachments/assets/24410194-9af7-4feb-ac8c-36038aca65bd" />

## Accessing in your script

Minescript is split into classes for ease of maintenance and imports. 

Using the `Util` class as an example, below is a script to print out the hunger level of the player.

```python
from minescript_plus import Util
print(Util.get_food_level)
```
## Documentation

The documentation for minescript plus is available at:

[`https://github.com/R4z0rX/minescript-scripts/blob/main/Minescript-Plus/README.md`](https://github.com/R4z0rX/minescript-scripts/blob/main/Minescript-Plus/README.md)
