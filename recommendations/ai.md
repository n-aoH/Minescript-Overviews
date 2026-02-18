# Using AI alongside Minescript

AIs such as chatGPT can be used to help you when creating minescript, but they are still extremely limited.
I have found that their best usecase is to generate snippets of code for reference or that you're stuck on.

Don't use AI as a vibecoding tool, it will not be able to magically make a script for you without errors.
You will likely have to redirect chatGPT during advanced API tasks several times before getting the correct output.

For python issues, chatGPT is much more capable, given you tell it to give you a function to do `x` using `y` input.

## Sample ChatGPT Prompt (Python)

```
I am currently working on a project using the Python module minescript to integrate into minecraft.
I have access to minescript_plus.
Keep in mind that minescript does not support event decorators.
Minescript docs: https://minescript.net/docs
Keep your code to the documentation specs.

Please make a code snippet to get the name of every entity and return it as a list.
```

It's possible to get it to generate longer snippets, but you have to make sure that it has the actual documentation loaded instead of just halucinating java into it.

## Sample ChatGPT Prompt (Pyjinn Reference)

```
I am currently trying to find the correct Minecraft mappings to integrate into my minescript python script.
Here is a website for mappings: https://mappings.dev/1.21.11/index.html
Example mapping in python: BlockPos = JavaClass("net.minecraft.core.BlockPos")

Please generate a snippet that returns the player's maximum HP.
```

Pyjinn + mappings are extremely iffy on chatGPT. 

You will have to fanagle with it and likely give it some more reference code before it actually spits out something reasonable.
When in doubt, you can always use minescript_plus as a refrence for how to use these variables.

I do not recommend using chatGPT for Pyjinn references until you are experienced enough to be able to tell whenever it's going off course (which it will do extremely often).

## ChatGPT to fix Code

ChatGPT is much more capable of inferring what is going on whenever you ask it to fix your code instead of generate new code.

If you give it a snippet of your function (even using minescript) that isn't working, it is significantly more likely to correctly implement a pythonic solution that is by documentation standards.

## Conclusion

- Vibecoding will not work for minescript.

- Give chatGPT sufficient context

- Have an understanding of what you're doing before leaning on AI.

Entirely vibe-coded scripts are also difficult to provide help with (little context, frequent misunderstandings, no debugging), so please make sure that *you* are the one writing before you ask for help in the official Discord server.
