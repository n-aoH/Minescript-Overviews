# Rendering in the HUD
### What is the HUD?
The "Heads Up Display" is a collection of on-screen information, such as your hotbar, health, hunger or the `f3` menu etc.
## The following tutorial will:
- Show you `fabric`-s render callback
- Show you the `GuiGraphics` class, and its methods
- Teach you how to set up HUD rendering
- Teach you how to render simple shapes on the HUD
## The heart of HUD rendering: `HudRenderCallback`
Fabric exposes an event, similar to the `render` event from minescript, that lets you easily render shapes on the HUD: `net.fabricmc.fabric.api.client.rendering.v1.HudRenderCallback`

This event fires in the middle of rendering the HUD, and provides the necessary arguments to actually render.
## The magical class to render: `GuiGraphics`
`GuiGraphics` is the first argument that `HudRenderCallback` gives you, and it is what tells the game to draw shapes on the HUD.

The basic methods we will be using in this tutorial:
- `fill` Fills a rectangle of the screen with a solid color
- `drawString` Renders a piece of text, with a solid color

## HUD render setup
To render on the hud, we need to import the following classes (at minimum):
- `net.fabricmc.fabric.api.client.rendering.v1.HudRenderCallback`
- `net.minecraft.util.ARGB` (ARGB stands for Alpha-Red-Green-Blue, it is needed for colors)
- `net.minecraft.network.chat.Component` (Component is minecrafts "text" class. Needed for rendering text)
- `net.minecraft.client.Minecraft` (Specifically for the font. Needed for rendering text)
If you don't have mappings installed, install them with `\install_mappings`

## Render simple shapes
First, lets import all necessary classes
```py
mc = JavaClass("net.minecraft.client.Minecraft").getInstance()
HudRenderCallback = JavaClass("net.fabricmc.fabric.api.client.rendering.v1.HudRenderCallback")
ARGB = JavaClass("net.minecraft.util.ARGB")
Component = JavaClass("net.minecraft.network.chat.Component")
```
Then, lets set up our render event callback.

The game does not understand pyjinn functions, so we have to wrap it in something it can understand, like a `ManagedCallback` (builtin to pyjinn)
```py
def on_hud_render(GuiGraphics,_): # Note: the '_' is a delta time variable, we do not need
  # GuiGraphics functions go here

managed_callback = ManagedCallback(on_hud_render)
render_callback = HudRenderCallback(managed_callback)
HudRenderCallback.EVENT.register(render_callback) # This is where we register the event
```
This will run whats in `on_hud_render` every frame.

To draw a rectangle, we will use `GuiGraphics.fill`

`GuiGraphics.fill(x_position_1, y_position_1, x_position_2, y_position_2, color)`
```py
# A square with a size of 50 pixels, starting at 100:100 (x:y), with a red color
GuiGraphics.fill(100, 100, 150, 150, ARGB.color(255, 255, 0, 0))
```
Colors are managed with `ARGB.color`:

`ARGB.color(Alpha, Red, Green, Blue)`

It is identical to normal RGB, but with an `Alpha` variable, that controlls its opacity (0 is fully seethrough, 255 is fully opaque)

To render a string, we use `GuiGraphics.drawString`

`GuiGraphics.drawString(font, Component, x_position, y_position, color)`
```py
# A string saying "Hello World" at 100:100 (x:y), with a color of blue
GuiGraphics.drawString(mc.font, Component.literal("Hello World"), 100, 100, ARGB.color(255, 0, 0, 255))
```
## Putting it all together
Example script that renders a rectangle, that says "Hello World":
```py
mc = JavaClass("net.minecraft.client.Minecraft").getInstance()
HudRenderCallback = JavaClass("net.fabricmc.fabric.api.client.rendering.v1.HudRenderCallback")
ARGB = JavaClass("net.minecraft.util.ARGB")
Component = JavaClass("net.minecraft.network.chat.Component")

def on_hud_render(GuiGraphics,_):
  GuiGraphics.fill(99, 99, 156, 110, ARGB.color(255, 255, 0, 0))
  GuiGraphics.drawString(mc.font, Component.literal("Hello World"), 100, 100, ARGB.color(255, 0, 0, 255))

managed_callback = ManagedCallback(on_hud_render)
render_callback = HudRenderCallback(managed_callback)
HudRenderCallback.EVENT.register(render_callback)
```
<img width="266" height="86" alt="image" src="https://github.com/user-attachments/assets/723243e4-7680-4277-bf4e-f6b57559e697" />

# Good to know:
- The positions scale with your gui scale, where a gui scale of x divides the resolution by x. Example: A screen pixel coordinate of 100, 100 at gui scale 4, becomes 25, 25
- Ordering matters! Everything will render on the order you have in the functiom, meaning the last `GuiGraphics` call will be above all other
- Rendering an excessive amount can and will lag the game
- *Size* of rendered rectangles does NOT impact performance
- Most GUI-s will render on top of what you drew, and there is no way to bypass this without a dedicated mod
