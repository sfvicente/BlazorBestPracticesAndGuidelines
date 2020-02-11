# Components | General
<br>

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

**Use the `Parameter` attribute to specify arguments for a component in markup.**

```
<h1>@Title</h1>

@code {
	[Parameter]
	public string Title { get; set; }
}
```
<br><br>


**To render raw HTML on a page, use the `MarkupString` property.**

To render raw HTML, wrap the HTML content in a `MarkupString` value. The value is parsed as HTML or SVG and inserted into the DOM.

```
@page "/test"

<h1>Example: Raw HTML</h1>

@((MarkupString)markup)

@code{
	string markup = "<p>This is a <strong>Hello World</strong> example</p>";
}
```
<br><br>