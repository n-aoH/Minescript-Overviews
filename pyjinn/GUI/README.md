# GUI Tutorial

Here are a few snippets to help you add your own GUI objects to Minecraft.

## Adding Buttons to pre-existing GUIs

Below is a snippet and tutorial for adding your own buttons. Created from code by Razrcraft.

### Full snippet

```python
#!python
from system.pyj.minescript import *
Minecraft = JavaClass("net.minecraft.client.Minecraft")
ScreenEvents = JavaClass("net.fabricmc.fabric.api.client.screen.v1.ScreenEvents")
ScreenEventsAfterInit = JavaClass("net.fabricmc.fabric.api.client.screen.v1.ScreenEvents$AfterInit")
Screens = JavaClass("net.fabricmc.fabric.api.client.screen.v1.Screens")
Button = JavaClass("net.minecraft.client.gui.components.Button")
Component = JavaClass("net.minecraft.network.chat.Component") 

mc = Minecraft.getInstance()

def example_function(ctx): #first arg doesn't matter, just a random javaclass. Removing this will crash.
    echo("Yay, it works!")

def after_init(client, screen, scaledWidth, scaledHeight):
    if "Chat" in screen_name():

        # Positioning code
        x = int(scaledWidth / 2)
        y = int(scaledHeight / 2)
        width = 50
        height = 20
        name = "Example"


        #Button cunstructor
        Screens.getButtons(screen).add(Button.Builder(Component.literal(name), example_function).pos(x, y).size(width, height).build())

afterinit_callback = ManagedCallback(after_init) 
ScreenEvents.AFTER_INIT.register(ScreenEventsAfterInit(afterinit_callback))
```

### Explanation

Above is the starting code.

The imports at the top are necessary to initalize your JavaClass methods.

The `example_function()` can be called from the button, with one passed argument that is discarded.

The `after_init()` function is called once upon the screen opening, meaning that this tutorial will not work for dynamically moving objects.

You can use the button constructor method as many times as you want.

