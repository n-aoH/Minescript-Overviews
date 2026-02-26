# Script Arguments

## sys.argv

Scripts can recieve arguments from the command-line (beginning chat execution in this case) through the sys.argv API.

When your script launches, sys.argv will provide a list of the below information:
```py
sys.argv[0] # Script name (argument 0)
sys.argv[1] # Arg 1
sys.argv[2] # Arg 2
sys.argv[3] # Arg 3
...
```

Here's a simple script that will repeat the first argument back to you:

```py
# repeat_to_me.py
import sys

print(sys.argv[1])
```

But if you run it without any arguments, you'll get an error.
This is one of the things that you have to catch before the user makes the mistake so that python doesn't get mad at you.

```py
import sys

if len(sys.argv) > 1:
  print(sys.argv[1])
else:
  print("Please provide an argument!")
```

If you just want to see if an argument is present (ex. `no_log`) you can check if it's in the list.

```py
if "-no_log" in sys.argv:
  logging = False
else:
  logging = True
```

Often times, script arguments will start with a dash to differentiate themselves to make sure that one argument can't trigger two triggers.
