# Components | Rendering
<br>


### To render components dynamically, use `if-else` or `switch-case` conditional statements in _Razor_ view code.

You can use and render different components for different scenarios. Displaying components dynamically can be done with if-else or switch-case conditions and through the use of variables.

TODO: Example

It is also possible to render components dynamically at the application level.

```csharp
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


### Do not use `StateHasChanged()` to force the render of components in synchronous methods.

```csharp
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

```csharp
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


### To Suppress UI refreshing, override `ShouldRender()` and return `false`.

The `ShouldRender()` method is called each time the component is rendered. You can override `ShouldRender()` to prevent the UI from refreshing.
If the implementation returns  `true`, the UI is refreshed, otherwise, refresh is suppressed.

```csharp
protected override bool ShouldRender()
{
    return false;
}
```
Even if  `ShouldRender()`  is overridden, the component is always initially rendered.
<br>


### Use `@key` whenever a list such as a `@foreach` block is rendered and a suitable value exists to define the `@key`.

```csharp
// ToDo: Example
```
<br><br>


### Use `@key` to prevent Blazor from preserving an element or component subtree when an object changes.

```csharp
// ToDo: Example
```
<br><br>


### Do not to use @key when there's a performance cost when diffing with  `@key`.

```csharp
// ToDo: Example
```

The performance cost isn't large, but only specify `@key` if controlling the element or component preservation rules benefit the app.
<br><br>


### Only use distinct values, such as object instances or primary key values.

```csharp
// ToDo: Example
```
<br><br>


## Component Virtualization

<Virtualization is a technique for limiting the UI rendering to just the parts that are currently visible. A common example is when an application has a long list or table with 
many rows and only a small subset is visible at any given time.>


### Improve the perceived performance of component rendering using the built-in virtualization support.

 Blazor has a `Virtualize` component that can be used to add virtualization to components.

A typical list or table-based component might use a C# foreach loop to render each item in the list or each row in the table, like this:

```csharp
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

```csharp
<Virtualize Items="employees" Context="employee">
    <tr>
        <td>@employee.FirstName</td>
        <td>@employee.LastName</td>
        <td>@employee.JobTitle</td>
    </tr>
</Virtualize>
```

The `Virtualize` component calculates how many items to render based on the height of the container and the size of the rendered items.

Reference: https://devblogs.microsoft.com/aspnet/asp-net-core-updates-in-net-5-release-candidate-1/
Additional Tags: Performance

