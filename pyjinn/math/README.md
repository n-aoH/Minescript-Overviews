# Doing math in Pyjinn

## No python modules

Pyjinn is compiled into Java, meaning that it has some limitations. One of these is that you cannot use the built-in python modules such as `math`.

To get around this, you can still use Java's built-in math library.

## Initializing

To initialize Java's math module, simply include the following line in your pyjinn file.

```
Math = JavaClass("java.lang.Math")
```

## Documentation

To find available functions, visit:

`https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Math.html`

## Accessing

This `Math` module can be accessed similarly to the python module.

```
x_offset = Math.sin(20) * radius
```

As a reminder, all trig functions use radians as their unit of measurement, not degrees. Convert between them with `Math.toRadians(degrees)`

# Alternative solution

I have also created a drop-in replacement for the `math` module in python if you would like to access it in VS Code (or other IDES) automatically instead of using the java documentation.

https://github.com/n-aoH/minescript-projects/blob/main/pyjinn-utils/math_pyj.py

It can be imported as:
```python
import math_pyj as math
```

And from there, it's the same as using the math module.
