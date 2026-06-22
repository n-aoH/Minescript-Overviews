# Drawing with Gizmos

This guide will go over the basics of drawing elements in the world with Gizmos, and then show the rendering of gizmos around entities.

## What are Gizmos?

Gizmos are Minecraft's 1.21.11+ API for world rendering, and are significantly easier to use than the older API. They also function as a great way to get into Pyjinn if you have the boilerplate.

## Drawing a box

This overview will use Razr's wiki page [here](https://github.com/n-aoH/Minescript-Overviews/blob/dev/pyjinn/Gizmos%20Rendering.md). Feel free to reference it.

At the top of the script, you can copy and paste some JavaClass definitions that we'll use later.

```py
#!python
from minescript import *

# Required Java classes
Gizmos          = JavaClass("net.minecraft.gizmos.Gizmos")
GizmoStyle      = JavaClass("net.minecraft.gizmos.GizmoStyle")
TextGizmo_Style = JavaClass("net.minecraft.gizmos.TextGizmo$Style")
BlockPos        = JavaClass("net.minecraft.core.BlockPos")
Vec3            = JavaClass("net.minecraft.world.phys.Vec3")
AABB            = JavaClass("net.minecraft.world.phys.AABB")
Direction       = JavaClass("net.minecraft.core.Direction")
ARGB            = JavaClass("net.minecraft.util.ARGB")
```

Usually, JavaClasses are defined at the start of scripts.

Next, here is the part that defines what `color` and `style` the boxes (and other gizmos) are drawn in, which we will pass in as arguments.

```py
color       = ARGB.color(255, 0, 200, 255)
fill_color  = ARGB.color(60,  0, 200, 255)
style       = GizmoStyle.stroke(color)
filled      = GizmoStyle.strokeAndFill(color, JavaFloat(1.5), fill_color)
```

As you can see, `color` is an ARGB value (Alpha / Transparency, Red, Green, Blue) that takes 4 integers respectively.

`style` is just an outline, while `filled` will draw both the inside and outside.

Now, we'll get into actually rendering a box, which is only 3 lines from here!

```py
def on_render(event):

    Gizmos.cuboid(BlockPos(10, 64, 10), filled)

add_event_listener("render",on_render)
```
Now, if you run this script and teleport to `10, 64, 10`, you will see the box!

<img width="467" height="406" alt="image" src="https://github.com/user-attachments/assets/3174dcf8-da95-4073-bb6b-b9615cb23bfd" />

But what if you wanted to draw any size of box, and not just one at a set of coordinates?

## New constructors?

Luckily, the `Gizmos.cuboid` has 4 different constructors to use!

Checking it on the [mappings.dev page](https://mappings.dev/1.21.11/net/minecraft/gizmos/Gizmos.html),

<img width="799" height="448" alt="image" src="https://github.com/user-attachments/assets/eea79515-ad69-4887-b1e3-4e96005d33f6" />

We see 4 different constructors.

There's the one we just used: `cuboid(BlockPos arg0, GizmoStyle arg1)`

And one that will allow us to draw any cube: `cuboid(AABB arg0, GizmoStyle arg1)`

Mappings.dev (for 1.21.11-)
and mcsrc.dev (for 1.26+)

Are generally the two best ways to explore what JavaClasses you can use and how to use them. I prefer mappings.dev, even on 1.26.

Let's use the top constructor from mappins.dev: `cuboid(AABB arg0, GizmoStyle arg1)`

In order to make a box, we need to initialize AABB and then pass it into there instead of the blockpos.

Luckily, AABB are extremely easy to make:
```py
box = AABB(9, 63, 9, 11, 65, 10)
```

And then, you can simply swap out the `BlockPos` for the box.

```py
def on_render(event):

    box = AABB(9, 63, 9, 11, 65, 10)
    Gizmos.cuboid(box, filled)

add_event_listener("render",on_render)
```

Running this, you'll now have a rectangle rendered!

<img width="460" height="427" alt="image" src="https://github.com/user-attachments/assets/93ecd2a6-f34d-4457-8d47-d74931158e7a" />

Believe it or not, we're actually only a few lines away from rendering these boxes around entities!


## Putting it all together

Let's assess how we would render a box around every entity on the screen:
1. loop through every entity using `get_entities()`
2. create an AABB to represent each entity
3. make a cuboid from the AABB

As a reminder, each Gimzo call has to happen inside a render event if you're planning on making them update each frame.

This part should be firmiliar to you, as we get the position of each entity
```py
def on_render(event):
    for entity in get_entities():
        pos = entity.position
        x = pos[0]
        y = pos[1]
        z = pos[2]
```
And then pass them into each box:
```py
        box = AABB(x-.5, y, z-.5, x+.5, y+2, z+.5) # 1 width, 1 length, 2 height on these boxes
        Gizmos.cuboid(box, filled)
```

Combining this, we've finally drawn the boxes!

Feel free to play around with more rendering settings, like fadeout time, persistence, and being on the top layer (covered in the wiki page)!

Of course, the boxes don't show the hitbox, but that's as far as you can go without diving deeper into JavaClasses and `Java` entity references (which will be covered later).

You can add onto this, changing the color based on the `entity.type`.
