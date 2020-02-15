# Components | Rendering
<br>


### Usage of the  `StateHasChanged()`


**CDxxx - Do not use `StateHasChanged()` to force the render of components in synchronous methods.**

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





### Usage of the  `@key`

**CS010 - Use `@key` whenever a list such as a `@foreach` block is rendered and a suitable value exists to define the `@key`.**

```csharp
    ToDo: example
```

**CS011 - Use `@key` to prevent Blazor from preserving an element or component subtree when an object changes**

```csharp
    ToDo: example
```

**CD0xx - Do not to use @key when there's a performance cost when diffing with  `@key`.**

```csharp
    ToDo: example
```

The performance cost isn't large, but only specify  `@key`  if controlling the element or component preservation rules benefit the app.


**CS012 - Only use distinct values, such as object instances or primary key values**

```csharp
    ToDo: example
```