# Components | Rendering
<br>


## General
<br>

### To render components dynamically, use `if-else` or `switch-case` conditional statements in _Razor_ view code.

You can use and render different components for different scenarios. Displaying components dynamically can be done with if-else or switch-case conditions and through the use of variables.

TODO: Example

It is also possible to render components dynamically at the application level.

```cs
<app>
	@if(condition == 1)
	{
		<Component1/>
	}
	else if (condition == 2)
	{
		<Component2/>
	}
	else
	{
		<Component3/>
	}
</app>
```
<br>


## Markup
<br>

### To render raw HTML on a page, use the `MarkupString` property.

To render raw HTML, wrap the HTML content in a `MarkupString` value. The value is parsed as HTML or SVG and inserted into the DOM.

```cs
@page "/test"

<h1>Example: Raw HTML</h1>

@((MarkupString)markup)

@code{
	string markup = "<p>This is a <strong>Hello World</strong> example</p>";
}
```
<br>


## `StateHasChanged` Method

The `StateHasChanged` is a method of the `ComponentBase` that notifies the component that its state has changed.


### Do not use `StateHasChanged()` to force the render of components in synchronous methods.

```cs
<button @onclick="@PlaceOrder_Clicked" disabled="@DisablePlaceOrderButton">Place Order</button>

@code {
 private bool DisablePlaceOrderButton { get; set; } = false;

 private void PlaceOrder_Clicked()
    {
        DisablePlaceOrderButton = true;
        StateHasChanged();

        if (cart.Lines.Count() == 0)
        {
            DisablePlaceOrderButton = false;
            return;
        }
        ...
}
```
In this example button will be disabled only after PlaceOrder() method finishes executing. 

StateHasChanged informs the component that its state has changed but it does not render the component. The component will decide when to render itself. You can't do that in a synchronous method, you should async your code to let the component a chance to render.

```cs
<button @onclick="@PlaceOrder_Clicked" disabled="@DisablePlaceOrderButton">Place Order</button>

@code{
    private bool DisablePlaceOrderButton { get; set; } = false;

    private async Task PlaceOrder_Clicked()
    {
        DisablePlaceOrderButton = true;
        ...

    }
}
```
<br><br>


### To suppress UI refreshing, override `ShouldRender()` and return `false`.

The `ShouldRender()` method is called each time the component is rendered. You can override `ShouldRender()` to prevent the UI from refreshing. If the
method implementation returns `true`, the UI is refreshed, otherwise, refresh is suppressed.

```cs
protected override bool ShouldRender()
{
    return false;
}
```

However, even if `ShouldRender()` is overridden to return `false`, the component is always initially rendered.
<br>


## `@key` directive attribute

The `@key` directive attribute is a mechanism to control the mapping process of model objects to elements or components.
<br>


### Use `@key` whenever a list such as a `@foreach` block is rendered and a suitable value exists to define the `@key`.

TODO: complement description

```cs
@foreach (var user in Users)
{
    <UserEditor @key="user" Role="@user.Role" />
}

@code {
    [Parameter]
    public IEnumerable<User> Users { get; set; }
}

```
<br><br>


### Use `@key` to prevent Blazor from preserving an element or component subtree when an object changes.

```cs
// ToDo: Example
```
<br><br>


### Do not to use @key when there's a performance cost when diffing with  `@key`.

```cs
// ToDo: Example
```

The performance cost isn't large, but only specify `@key` if controlling the element or component preservation rules benefit the app.
<br><br>


### Only use distinct values, such as object instances or primary key values.

```cs
// ToDo: Example
```
<br><br>


## Component Virtualization

<Virtualization is a technique for limiting the UI rendering to just the parts that are currently visible. A common example is when an application has a long list or table with 
many rows and only a small subset is visible at any given time.>
<br>


### Use the built-in virtualization support to improve the perceived performance of component rendering.

 Blazor has a `Virtualize` component that can be used to add virtualization to components.

A typical list or table-based component might use a C# foreach loop to render each item in the list or each row in the table, like this:

```cs
@foreach (var employee in employees)
{
    <tr>
        <td>@employee.FirstName</td>
        <td>@employee.LastName</td>
        <td>@employee.JobTitle</td>
    </tr>
}
```

If the list grew to include thousands of rows, then rendering it may take a while, resulting in a noticeable UI lag.

Instead, you can replace the foreach loop with the `Virtualize` component, which only renders the rows that are currently visible.

```cs
<Virtualize Items="employees" Context="employee">
    <tr>
        <td>@employee.FirstName</td>
        <td>@employee.LastName</td>
        <td>@employee.JobTitle</td>
    </tr>
</Virtualize>
```

The `Virtualize` component calculates how many items to render based on the height of the container and the size of the rendered items.

Requires: .NET 5 RC1
Reference: https://devblogs.microsoft.com/aspnet/asp-net-core-updates-in-net-5-release-candidate-1/
Additional Tags: Performance
<br>


### Specify an `ItemsProvider` when performing virtualization to prevent loading all items into memory.

To avoid loading all the items from a data source into memory, specify an `ItemsProvider` when defining the `Virtualize` component:

```cs
<Virtualize ItemsProvider="LoadUsers" Context="user">
     <tr>
         <td>@user.FirstName</td>
         <td>@user.LastName</td>
         <td>@user.Email</td>
         <td>@user.DateRegistered</td>
    </tr>
</Virtualize>
```

<An items provider is a delegate method that asynchronously retrieves the requested items on demand. The items provider receives an ItemsProviderRequest, which specifies
the required number of items starting at a specific start index. The items provider then retrieves the requested items from a database or other service and returns them as an 
ItemsProviderResult<TItem> along with a count of the total number of items available.>

<
```cs
async ValueTask<ItemsProviderResult<Employee>> LoadEmployees(ItemsProviderRequest request)
{
    var numEmployees = Math.Min(request.Count, totalEmployees - request.StartIndex);
    var employees = await EmployeesService.GetEmployeesAsync(request.StartIndex, numEmployees, request.CancellationToken);
    return new ItemsProviderResult<Employee>(employees, totalEmployees);
}
```
>

Requires: .NET 5 RC1
Reference: https://devblogs.microsoft.com/aspnet/asp-net-core-updates-in-net-5-release-candidate-1/
Additional Tags: Performance
<br>


### Consider caching data in the items provider so it is readily available.

The items provider method is used to retrieve the required items. It can either retrieve data with each request or include a caching mechanism to prevent trips to the data source.

```cs
async ValueTask<ItemsProviderResult<Post>> LoadPosts(ItemsProviderRequest request)
{
    var postCount = Math.Min(request.Count, totalPosts - request.StartIndex);
    var posts = await PostsService.GetPostsAsync(request.StartIndex, postCount, request.CancellationToken);

    //TODO: Add caching code

    return new ItemsProviderResult<Post>(posts, totalPosts);
}
```

Requires: .NET 5 RC1
Additional Tags: Performance
<br>


### Use a placeholder to render temporary elements while waiting for the item data to become available.

The `Virtualize` component allows the use of a placeholder to denote the temporarily missing data.

This can be used to improve perceived performance. It especially useful when requesting information from remote or slow data sources.

```cs
<Virtualize ItemsProvider="LoadUsers" Context="user">
    <ItemContent>
        <tr>
            <td>@user.FirstName</td>
            <td>@user.LastName</td>
            <td>@user.Email</td>
            <td>@user.DateRegistered</td>
        </tr>
    </ItemContent>
    <Placeholder>
        <tr>
            <td>Loading...</td>
        </tr>
    </Placeholder>
</Virtualize>
```

Additional Tags: Performance
Requires: .NET 5 RC1
<br>


### Invoke `StateHasChanged` when changes are made to the items rendered in a `Virtualize` component to force re-evaluation and rerendering of the component.

Invoking `StateHasChanged()` after modifying the items rendered in a virtualized component is essential to maintaining a
responsive and accurate user interface in Blazor applications. By explicitly triggering a re-evaluation and re-rendering
of the component, you ensure that changes to the underlying data are reflected in the virtualized UI, providing a seamless
and efficient user experience.

```csharp
@page "/virtualized-list"

<Virtualize Context="item">
    <div>@item</div>
</Virtualize>

<button @onclick="AddItem">Add Item</button>

@code {
    private List<string> items = new List<string> { "Item 1", "Item 2", "Item 3" };

    private void AddItem()
    {
        items.Add($"Item {items.Count + 1}");

        // Call StateHasChanged to force re-evaluation and re-rendering
        StateHasChanged();
    }
}
```

Requires: .NET 5 RC1
Additional Tags: `StateHasChanged` Method
<br><br>


## `ShouldRender` Method
The `ShouldRender` method of the `ComponentBase` class determines whether a component should re-render based on changes
in its state or parameters.
<br>


### Configure `ShouldRender` to return `false` when developing UI-only components that won't change after the initial render.

If a UI-only component doesn't change after being rendered the first time, the `ShouldRender` should be set to `false`. This prevents re-rendering of the component and associated
cost for the application.

```cs
@code {
    protected override bool ShouldRender() => false;
}
```

Additional Tags: Lifecycle, Performance
<br>


### Use private fields to manually control the `ShouldRender` method to prevent rendering of exceptionally expensive subtrees that degrade UI performance.

Using private fields to manually control the `ShouldRender` method allows developers to optimize rendering performance
in components, especially when dealing with complex UIs or expensive rendering operations. By selectively triggering
re-renders based on specific conditions or state changes, you can minimize unnecessary updates and improve the overall
responsiveness of applications.

```csharp
public class ExpensiveRenderingComponent : ComponentBase
{
    private int _counter = 0;
    private bool _shouldRender = true;

    protected override bool ShouldRender()
    {
        return _shouldRender;
    }

    private void IncrementCounter()
    {
        _counter++;
        // Manually control when to trigger a re-render
        if (_counter % 5 == 0)
        {
            _shouldRender = true; // Render every 5th increment
        }
        else
        {
            _shouldRender = false; // Skip rendering for other increments
        }
    }

    protected override void BuildRenderTree(RenderTreeBuilder builder)
    {
        builder.OpenElement(0, "div");
        builder.AddContent(1, $"Counter value: {_counter}");
        builder.CloseElement();
    }
}
```

Additional Tags: Lifecycle, Performance
<br>


## Integration
<br>


### To render components in a page or view, use the Component Tag Helper.

You can integrate _Razor_ components and views into _Razor Pages_ using the Component Tag Helper.

todo: complement description

```cs
@page
@model RegisterModel
@{
    ViewData["Title"] = "Register";
}

<h1>@ViewData["Title"]</h1>

<component type="typeof(RegisterBenefits)" render-mode="Static" />

...

@section Scripts {
    <partial name="_ValidationScriptsPartial" />
}
```

Additional Tags: Razor Pages, Component Tag Helper
<br>