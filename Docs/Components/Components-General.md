# Components | General
<br>

## Naming Conventions

A naming convention is an agreed scheme for naming items.
<br>


### Use PascalCase for naming components.

A component name is required to start with an uppercase character. Create component names by concatenating capitalized words:

```
NavMenu.razor

```
<br>


### Use the `Razor` code block notation to be able to use quotes inside component declarations.

You can use the parenthesis @( ) to create a code block. This will allow quotes to be used inside the component declaration.

```csharp
<MyComponent User="@context.User.Claims.Where(user => user.Type == "administrator")"></MyComponent>
```
<br>

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
<br>


## Namespaces

Namespaces are mechanisms to organize and control the scope of program elements in application projects.
<br>


### Add the `@using` directive in the an __Imports.razor_ file at any level file to make a library's components available to a single page or set of pages within a folder.

```csharp
@using MyComponent

```
<br>


### Do not use the loop variable in a `for` loop directly in a lambda expression.

The following code should not be used:

```csharp
// ToDo: Example
```

Using the same variable used by all lambda expressions causes `i`'s value to be the same in all lambdas. Always capture its value in a local variable before using it.

```csharp
// ToDo: Example
```
<br>


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
<br>


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
<br>


## Inheritance
<br>


### Use the `@inherits` directive to allow a component to inherit from a base class.

```csharp
using Microsoft.AspNetCore.Components;

namespace MyNamespace
{
    public class MyBaseComponent : ComponentBase
    {
        public string Title { get; set; } = 
            "My Application";
    }
}
```

When developing the base class, it should derive from `ComponentBase`. Use the `@inherits` directive on the subclass to inherit the component's properties and methods:

```csharp
@page "/SubComponent"
@inherits MyBaseComponent

<h1>@Title</h1>
```

<br>


## Component Parameters

Component parameters are values passed to the component that are required to execute and complete tasks.
<br>


### Use the `Parameter` attribute to specify arguments for a component in markup.

```csharp
<h1>@Title</h1>

@code {
	[Parameter]
	public string Title { get; set; }
}
```
<br>


### To determine if a component parameter has been assigned a value, override the `SetParametersAsync()` method and inspect the parameter collection.

When you create a component, it's possible to add parameters to allow passing information to the component. Consider the following component:

```csharp
<h1>@Title</h1>

@code {
	[Parameter]
	public Foo Foo { get; set; }
}
```

The component can be added to the application and it's parameter can be used as in the example below:

```csharp
<MyComponent Foo="@foo" />

@code {
    public Foo foo { get; set; }
}
```

You can also choose to use the component but unlike the previous example, decide not to assign an argument to the `Foo` parameter.

```csharp
<MyComponent />
```
In this case, the parameter is omitted. As a component can be used both ways, it may be necessary to determine whether the parameter was assigned a value or not.

You can override the `SetParametersAsync()` method and iterate through the 'parameters' collection to determine if the parameter has been passed to the component.
A parameter that hasn't been specified will not be present in the collection.

```csharp
@code {

    [Parameter]
    public Foo Foo { get; set; }

    public override async Task SetParametersAsync(ParameterView parameters)
    {
        foreach(var p in parameters)
        {
            if(p.Name == "Foo")
            {
                System.Diagnostics.Debug.WriteLine($"Value: {p.Value?.ToString()}");
            }
        }

        await base.SetParametersAsync(parameters);
    }
}
```
<br>


## Child Content
<br>


### To allow a component to accept content for rendering, create a parameter named `ChildContent` of type `RenderFragment`.

Components can be configured by other components through the use of parameters. However to set child content for rendering, a component can use parameters of
type `RenderFragment`. By convention, it is required that the property is named `ChildContent`.

Below is the example of a content that can accept child content for rendering:

```csharp
<div>
    <h1>@Title</h1>
    <div>@ChildContent</div>
</div>

@code {
    [Parameter]
    public string Title { get; set; }

    [Parameter]
    public RenderFragment ChildContent { get; set; }
}
```

The component can be set from the parent in the following way:

```csharp
@page "/ParentComponent"

<h1>My Parent Component</h1>

<ChildComponent Title="MyTitle">
    Content to be set in the child component provided by the parent component.
</ChildComponent>
```

<br>


## Cascading Values
 
Cascading values is a component that allows values passed to it to be cascaded down its component tree to all of its descendants.
<br>


### To use content from cascading values in a component, declare a property of the same type, decorated with the `[CascadingParameter]` attribute.

The code below setups cascaded values for the component.

```csharp
<CascadingValue Value="@Username">
    <MyComponent></MyComponent>
</CascadingValue>

@code {
    string Username = "admin";
}
```

To access the information, declare a property of the same type within the component. Decore the property with the `[CascadingParameter]` attribute.

```csharp
<h1>My Component</h1>

<p>Hello: @Username</p>

@code {
    [CascadingParameter]
    string Username { get; set; }
}
```

<br>