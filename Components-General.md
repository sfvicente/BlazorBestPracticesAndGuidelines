# Components | General
<br>


### Use PascalCase for naming components

Component names should be created by concatenating capitalized words.

```
NavMenu.razor

```
<br><br>


### Use the `@using` directive in the top-level __Imports.razor_ file to make a library's components available to an entire project.

```csharp
@using System.Net.Http
@using Microsoft.AspNetCore.Authorization
@using Microsoft.AspNetCore.Components.Authorization
@using Microsoft.AspNetCore.Components.Forms
@using Microsoft.AspNetCore.Components.Routing
@using Microsoft.AspNetCore.Components.Web
@using Microsoft.JSInterop

@using MyComponent
```
<br><br>


### Add the `@using` directive in the an __Imports.razor_ file at any level file to make a library's components available to a single page or set of pages within a folder.

```csharp
@using MyComponent

```
<br><br>


### Do not use the loop variable in a `for` loop directly in a lambda expression.

The following code should not be used:

```csharp
// ToDo: Example
```

Using the same variable used by all lambda expressions causes `i`'s value to be the same in all lambdas. Always capture its value in a local variable before using it.

```csharp
// ToDo: Example
```
<br><br>


### Use the `Parameter` attribute to specify arguments for a component in markup.

```csharp
<h1>@Title</h1>

@code {
	[Parameter]
	public string Title { get; set; }
}
```
<br><br>


### To render raw HTML on a page, use the `MarkupString` property.

To render raw HTML, wrap the HTML content in a `MarkupString` value. The value is parsed as HTML or SVG and inserted into the DOM.

```csharp
@page "/test"

<h1>Example: Raw HTML</h1>

@((MarkupString)markup)

@code{
	string markup = "<p>This is a <strong>Hello World</strong> example</p>";
}
```
<br><br>


### To assign a result of an `async` function to _razor_ component, use a property to store the value.

```csharp
@page "/"
@inject ICountingService Counter

<h1>Hello World!</h1>

<MyComponent Count="@CounterValue" />

@code{

     public int CounterValue {get; set;}
     protected override async Task OnInitalizedAsync()
     {
           CounterValue = await Counter.Get();
     }
}
```
<br><br>

