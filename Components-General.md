### Components | General

**Use PascalCase for naming components**

Component names should be created by concatenating capitalized words.

```
NavMenu.razor
```
<br><br>


**Do not use the loop variable in a `for` loop directly in a lambda expression.**

The following code should not be used:

`ToDo: Example`

Using the same variable used by all lambda expressions causes `i`'s value to be the same in all lambdas. Always capture its value in a local variable before using it.

`ToDo: Example`
<br><br>