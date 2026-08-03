# Guide Start

Welcome! This is the start of the pathfinding guide.

This guide will cover the basics of flood fill, and the next guide will cover actually creating a path from point A to point B.

## Starting Boilerplate

For this pathfinder, I'll use Pyjinn. You're free to make your own in python, but Pyjinn has higher performance and built in rendering APIs.

```py
File: pathfinder.pyj
-------
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

mc = JavaClass("net.minecraft.client.Minecraft").getInstance()

Instant = JavaClass("java.time.Instant")

color       = ARGB.color(0, 0, 200, 255)
fill_color  = ARGB.color(50,  0, 200, 255)
style       = GizmoStyle.stroke(color)
filled      = GizmoStyle.strokeAndFill(color, JavaFloat(1.5), fill_color)
```

As you can see, it's the standard rendering JavaClasses, in addition to a new `Instant` class from Java. Since Pyjinn doesn't have Python's `Time` module, we have to get creative with Java's `Instant` (of time) class.

The next bit of boilerplate that you need to write starts actually getting into creating and finding nodes.

```py
start = get_player().position
start[0] = int(start[0])
start[1] = int(start[1])
start[2] = int(start[2])
start = tuple(start)
```

First, we align the player to the Minecraft's block grid, which will be what we path find on.

```py
node_queue = [start]

explored_nodes = set(start)
valid_nodes = set()

MAX_NODES = 100
```

## Flood Filling
In all of the searching algorithms, you create a `queue` of nodes to attempt to process. 
All flood fill does is attempts to spread out as far as possible from a starting point by only making moves that are legal.

In addition, `explored_nodes` will be all the nodes that the pathfinder has already touched. Once the flood filler has checked a node, it never needs to revisit it again.

`valid_nodes` will be all the nodes that the pathfinder has successfully pathed to, and will be rendered at the end.

```py
def process():
    global node_queue
    while len(node_queue) > 0 and len(valid_nodes) < MAX_NODES:
        node = node_queue.pop(0)
        
        if "air" in getblock(*node):
            valid_nodes[node] = True
            
            try_to_add(node,[1,0,0]) #First argument: node position, Second Argument: offset
            try_to_add(node,[-1,0,0])
            try_to_add(node,[0,0,1])
            try_to_add(node,[0,0,-1])
```

Let's start off with the main processing function. All we need to do is continue processing the queue until either:
- A: The Queue is empty (We found all the area, yay!)
- B: We scanned enough nodes (Prevents a crash when the fill escapes the regular bounds).

When we go through the queue, we simply take the first instruction from the queue and check to see if it's air (which in this case means traversable).
If it is air, we add it to valid_nodes, which can be rendered, and then add its neighbors to the queue of things to visit.

Now, we just need to try to add them to the queue, if they haven't been explored already.

```py
def try_to_add(node, direction):
    global node_queue

    test_node = [0.0,0.0,0.0]
    test_node[0] = float(direction[0] + node[0])
    test_node[1] = float(direction[1] + node[1])
    test_node[2] = float(direction[2] + node[2])
    test_node = tuple(test_node)
    if not test_node in explored_nodes:
        explored_nodes.add(test_node)
        node_queue.append(test_node)
```
Here, all we do is add the offset `direction` to the starting node's position, then compare it to see if it has already been explored. 
If it hasn't, it can be added to the node queue and marked as explored.

Believe it or not, we're almost there. All we need to do is add the rendering and then time how long it took to path find it.

```py
def on_render(event):
    
    for pair in valid_nodes:
        x,y,z = pair
        box = AABB(x,y,z,x+1,y+1,z+1)
        Gizmos.cuboid(box, filled).setAlwaysOnTop()
```

If you care to learn about it, it's constructing a box using the valid nodes to position it, then making it always on top to be viewed easier.

```py
start = Instant.now().toEpochMilli()
process()
end = Instant.now().toEpochMilli()
print(f"Time taken: {end-start}ms")
print(f"Node Amount: {len(valid_nodes)}")

add_event_listener("render",on_render)
```

Timing it is relatively simple, just getting the current time before the process is started and then comparing it to the time after it ends.

## What's next?

After all that work, you've successfully created a flood fill algorithm! It's the predecessor to Breadth First Search (BFS). 
Where BFS differs is that it only stops whenever it finds a valid path to the target instead of when the network gets too large, storing the path it took through the nodes and eventually returning that.

This flood fill algorithm works well at showing where is walkable, and will easily show if a maze is completable. 
<img width="617" height="440" alt="image" src="https://github.com/user-attachments/assets/738e1e73-6c6a-484d-8411-781571df7475" />

When using Flood Fill and BFS, it is **Extremely Important** to keep the search area confined. These algorithms will quickly explode in node size with exponential growth, crashing the game if you turn MAX_NODES up too high.
