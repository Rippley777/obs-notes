# Variable Names

Variable names can _not_ have spaces, they're continuous strings of characters.

The creator of the Python language himself, [Guido van Rossum](https://en.wikipedia.org/wiki/Guido_van_Rossum), [implores us](https://peps.python.org/pep-0008/#function-and-variable-names) to use `snake_case` for variable names. What _is_ snake case? It's just a style for writing variable names. Here are some examples of different casing styles:

| Name        | Description                                                     | Code             | Language(s) that recommend it |
| ----------- | --------------------------------------------------------------- | ---------------- | ----------------------------- |
| Snake Case  | All words are lowercase and separated by underscores            | `my_hero_health` | Python, Ruby, Rust            |
| Camel Case  | Capitalize the first letter of each word _except the first one_ | `myHeroHealth`   | JavaScript, Java              |
| Pascal Case | Capitalize the first letter of each word                        | `MyHeroHealth`   | C#, C++                       |
| No Casing   | All lowercase with no separation                                | `myherohealth`   | No one: don't do this         |


# Parameters vs. Arguments

Parameters are the names used for inputs when _defining_ a function. Arguments are the values of the inputs supplied when a function is _called_.

To reiterate, **arguments are the actual values** that go into the function, such as `42.0`, `"the dark knight"`, or `True`. **Parameters are the names** we use in the function definition to refer to those values, which at the time of writing the function, can be whatever we like.

That said, this is all semantics, and frankly developers are really lazy with these definitions. You'll often hear the words "arguments" and "parameters" used interchangeably.