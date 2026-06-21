# Drawing with Gizmos

This guide will go over the basics of drawing elements in the world with Gizmos.

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

