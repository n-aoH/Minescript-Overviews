# Particle creation in pyjinn

Here is a guide on creating particle effects in pyjinn.

In this guide, we will create custom player particle effects in a script.



## Getting started

Before we start, make sure that your file ends in `.pyj` instead of `.py` to make sure that your project will be compiled in pyjinn.

Below is boiler plate code to start your script.

```python
#!python # makes your IDE recognize it's python
from system.pyj.minescript import * # makes your IDE show the actual pyjinn imports
Minecraft = JavaClass("net.minecraft.client.Minecraft") #accessing the world
ParticleTypes = JavaClass("net.minecraft.core.particles.ParticleTypes") #needed to reference particles

Math = JavaClass("java.lang.Math") #needed for trig 

mc = Minecraft.getInstance() #getting the client itself
```

Now, let's get a function for creating particles for now, it'll just be a wrapper so that your IDE will help you autocomplete it.

```python
def add_particle(type, x, y, z, xv, yv, zv)
  mc.level.addParticle(type, x, y, z, xv, yv, zv)
```

To test this out, Here's a starter script to spawn one particle down just below you.

```python
pos = get_player().position
pos[1] += 1
add_particle(ParticleTypes.END_ROD,*pos,0,0,0)
```

## Particle reference

A list of particles in your minecraft version can be found in a website/listing such as `mappings.dev`

The link I am specifically using is: https://mappings.dev/1.21.10/net/minecraft/core/particles/ParticleTypes.html

## Using Math

The Java `Math` module can be accessed from the Math variable using statements from https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Math.html

Example usage:
```python

degree = Math.toRadians(tick)

xv = Math.sin(degree/10) * 3
zv = Math.cos(degree/10) * 3
```

## Example programs

Here are a few programs I have made if you want some more guidance on starting to use particles.

**⭐Tip: Don't use while: True loops in pyjinn! It will crash!**

Flame Wall Aura:
```python

tick = 0

number_particles = 19
offset = 360/number_particles

def spawn_particle(ctx):
    global tick
    tick += 15
    pos = get_player().position
    
    degree = Math.toRadians(tick)

    
    # First Layer
    for i in range(number_particles-1):

        xv = Math.sin(degree/10) * 3
        zv = Math.cos(degree/10) * 3

        add_particle(ParticleTypes.FLAME,pos[0]+xv,pos[1],pos[2]+zv,0,.2,0)

        add_particle(ParticleTypes.FLAME,pos[0]-xv,pos[1],pos[2]-zv,0,.2,0)

        degree += offset


    degree = Math.toRadians(tick)
    pos[1] += 3


    # Second Layer
    for i in range(number_particles-1):
        
        
        xv = Math.sin(degree/10) * 3
        zv = Math.cos(degree/10) * 3

        add_particle(ParticleTypes.FLAME,pos[0]+xv,pos[1],pos[2]+zv,0,-.2,0)

        add_particle(ParticleTypes.FLAME,pos[0]-xv,pos[1],pos[2]-zv,0,-.2,0)

        degree += offset



add_event_listener("tick",spawn_particle)
```

Impact on fall:
```python
falling = False

def impact(ctx):
    global falling

    pos = get_player().position
    if falling and mc.player.fallDistance == 0: #jumping down
        
        
        pos[1] += .2
        add_particle(ParticleTypes.GUST,*pos,0,0,0)
    

    falling = (mc.player.fallDistance > 3)
    if falling:
        add_particle(ParticleTypes.FIREWORK,*pos,0,0,0)
    print(falling)

add_event_listener("tick",impact)
```




