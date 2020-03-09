# Components | Rendering
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

