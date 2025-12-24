# Minescript JavaClass Overview

This guide was created for minescript to provide starter information on the JavaClass() function.

## Mappings

Assuming you are on minescript release 5.0b or later, you can run `\install_mappings` in your chat to load them in.

This is a necessary step (for obfuscated versions) that tells your client what name goes in a human-readable format instead of something like `a(acs arg0)`

## Finding built-in JavaClasses

Now that you have installed the mappings, the next step is to find a JavaClass to reference.

Many JavaClasses in minecraft require other classes to work properly, so I reccommend finding boilerplate code for some common ones (ex: minecraft.getInstance() ) to help you while you are getting started.

The best library for mappings up to 1.21.11 is `mappings.dev`. Navigate to your version in the page to find the massive list of methods you can access.





## Accessing JavaClass()

Pyjinn has JavaClass automatically imported from `system.pyj.minescript`, but your .py files will require either `java` (recent versions) or `lib_java` (legacy)

Pyjinn:
```
from system.pyj.minescript import JavaClass #Technically not needed but your IDE gets less angry
```

Java:
```
from java import JavaClass
```

Lib_Java (legacy):
```
from lib_java import JavaClass
```

## Tutorial: accessing Minecraft.getInstance()

This tutorial will start with one of the first JavaClasses you will need to access for most of your player-based functions.

Under the mapping page for your version, `https://mappings.dev/1.21.10/index.html` for me, the fastest way to find most JavaClasses is to use `ctrl + F`. Use this to find `net.minecraft.client`.

<img width="297" height="256" alt="image" src="https://github.com/user-attachments/assets/2240370c-43de-4831-ac6e-eea7ddbb815a" />

There are several entries that include this, but you are looking for the entry that is specifically `net.minecraft.client`.

Inside your code, you can reference this as:
```
Minecraft = JavaClass("net.minecraft.client.Minecraft")
```

From here, you can access the `GetInstance` method in order to create a class of it.
```
mc = Minecraft.getInstance()
```

For many classes in Java, you must first create an instance of it before interacting. In this case, we do so with `Minecraft`.

## Pyjinn vs Java module

For time-sensitive applications, pyjinn will always be significantly better.

There is a delay in scripting when passing these objects between `Python -> Java -> Python -> Java` on seperate threads that will significantly slow your code down with .py files.

Pyjinn files don't have this issue because they're compiled into java and run natively, going from above to `Java -> Java -> Java -> Java` which is comparitively instant.

If you still require using Pyjinn files inside of a Python project, you can do so with embedded scripts, but I do not reccommend this for beginners.

## Tutorial: Set Velocity of player

**!!! This snippet uses code that will get you banned by anticheat on multiplayer servers. USE THIS AS AN EXAMPLE IN YOUR OWN SINGLEPLAYER WORLD !!!**

Using the above code to make a snippet:
```
Minecraft = JavaClass("net.minecraft.client.Minecraft")
mc = Minecraft.getInstance()
```

We can actually get in-game entity of the player from this snippet:
```Player = mc.Player```

From here, you can access any `public` method shown under `net.minecraft.world.entity` -> Class: `Entity` OR `net.minecraft.world.entity.player` -> Class: `Player` and edit these values.

There are some classes in these that do not overlap, so check each of them whenever you want to find something.

Let's take the `setDeltaMovement(double arg0, double arg1, double arg2)` method as an example.

<img width="889" height="143" alt="image" src="https://github.com/user-attachments/assets/a19ad888-df17-4fa5-8097-37f7fd9d1e10" />

You access these methods ingame using the Mojang mappings, similar to before:

```Player.SetDeltaMovement(0, 5, 0)```

Putting it all together:

```
Minecraft = JavaClass("net.minecraft.client.Minecraft")
mc = Minecraft.getInstance()

Player = mc.Player
Player.SetDeltaMovement(0, 5, 0)
```

Now, you've just made your first JavaClass script that accesses a method!
*note: The Player object gets reset every time you die, so make sure you re-reference it when needed.*

To reference a method that will return something (ex: `boolean`) you can reference it like any other variable/function in python.

Again, from the Entity class:
```
frozen_Percent = Player.getPercentFrozen()
echo("Frozen Percentage: "+frozen_Percent)
```

