# Components | Events
<br>


### To handle client-side UI events, specify an event attribute and declare an event handler in the component code.

Components can handle UI events by specifying both an event attribute and an event handler. Event attributes are defined inside an HTML tag. It requires the event name
and must be prepended with an @.

For example, to handle the `onclick` event in an input field, add the `onclick` as an attribute as shown below:

```csharp
<input @onclick="" />
```

In addition to specifying the event attribute, it is required to also declare an event handler. This can be achieved either inline:

```csharp
<p>Message: @Message</p>
<button @onclick="@((e) => {
    Message = "Hello World!";
})">Set Message</button>

@code {
    public virtual string Message { get; set; }
}
```

Or through a method within the `@code` section of the _Razor_ component:

```csharp
<p>Message: @Message</p>
<button @onclick="Click">Set Message</button>

@code {
    public virtual string Message { get; set; }

    public virtual void Click(MouseEventArgs e)
    {
        Message = "Hello World!";
    }
}
```

Additional Tags: Event Handler
<br>


### Use the `@on{EVENT}:stopPropagation` directive attribute to stop event propagation.

```csharp
<input type="text" value="" @onkeypress:preventDefault />
```
<br><br>


### Use both the `@on{EVENT}:stopPropagation` directive attribute and with your event handling to stop event propagation but still process your code.

```csharp
<input type="text" value="" @onkeypress="HandleKeyPresses" @onkeypress:preventDefault />
```
<br><br>


### To detect and handle mouse right-click events, use the `MouseEventArgs` property `Button`

```csharp
<div @onmouseup="HandleMouseUp" >
    div content
</div>

@code {
    void HandleMouseUp(MouseEventArgs args)
    {
        if (args.Button == 2)
            Console.WriteLine("This is a right click");
    }
}
```
<br><br>


### To handle mouse right-click events and not display the browser context menu, use the HTML `oncontextmenu` attribute

```csharp
<div oncontextmenu="return false;" @onmouseup="HandleMouseUp">
    div content
</div>

@code {
    void HandleMouseUp(MouseEventArgs args)
    {
        if (args.Button == 2)
            Console.WriteLine("This is a right click");
    }
}
```
<br>


### Use the `ontoggle` event to show or hide additional data of the `details` HTML element.

The `ontoggle` event occurs when the user opens or closes the `<details>` element. You can use the the `ontoggle` event to control the additional data contained in element.

```csharp
<div>
    @if (detailsExpanded)
    {
        <p>Read the details carefully!</p>
    }
    <details id="details-toggle" @ontoggle="OnToggle">
        <summary>Summary</summary>
        <p>Detailed content</p>
    </details>
</div>

@code {
    bool detailsExpanded;
    string message { get; set; }

    void OnToggle()
    {
        detailsExpanded = !detailsExpanded;
    }
}
```

Reference: https://devblogs.microsoft.com/aspnet/asp-net-core-updates-in-net-5-release-candidate-1/
<br>


### To detect each character input on a text box, use the `@oninput` event.

To capture every character being typed in a textbox, bind the `oninput` event with an input element. This trigger the event for each character input.

```csharp
<input type="text" @oninput="@HandleInput" />
```

Additional Tags: Events
<br>


### To handle the change of the selected item in a dropdown, use the `onchange` event attribute.

To capture a change in the selected item in a dropdown, add the `onchange` event attribute to the . When specifying the event handler, use a parameter of type `ChangeEventArgs`.

```csharp
@page "/select"

<label>Please select an option:</label>
<select @onchange="Select">
    <option value="">Please Select...</option>
    <option value="1">One</option>
    <option value="2">Two</option>
    <option value="3">Three</option>
</select>

<p>You selected: @SelectedOption</p>

@code {
    public virtual string SelectedOption { get; set; }

    public void HandleOptionChange(ChangeEventArgs changeEventArgs)
    {
        SelectedOption = changeEventArgs.Value.ToString();
    }
}
```

Additional Tags: UI, Dropdown
<br>


### To bind items in a collection to controls in a user interface structure such as table, use a loop with an event connected to a method that accepts the instance of item.

The code below binds each button of the table to functionality for the removal of the item from the collection.

```csharp
@page "/cart"

<h3>Cart</h3>

<table>
	<thead>
		<tr>
			<th>Product Name</th>
			<th>Edit</th>
			<th>Remove</th>
	</tr>
	</thead>
	<tbody>
	@foreach(var product in products)
	{
		<tr>
			<td>@product.Name</td>
			<td>@product.Quantity</td>
			<td>@product.Price</td>
			<td><button @onclick="@(() => Remove(product))">Remove</button></td>
		</tr>
	}
	</tbody>
</table>

@code {
	List<Product> products;

	...
	
    void Remove(Product product)
    {
		...
	}

    class Product
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public int Quantity { get; set; }
    }
}
```
<br>


### To define an asynchronous event handler, declare the handler as `async` with return type `Task`.

Event handlers can be defined as asynchronous by using the `async` keyword in the declaration and a return type of `Task`.

```csharp
<button class="btn btn-primary" @onclick="HandleAddToCart">
    Add To Cart
</button>

@code {
    private async Task HandleAddToCart(MouseEventArgs e)
    {
        await AddItemToCart();
    }
}

<br>


### Avoid using events that produce large amounts of data in _Blazor Server_ applications.

Example of DOM events that can produce excessive data are `oninput` and `onscroll`.

TODO: complement description

TODO: add code samples

Applies to: Blazor Server
Tags: Events, Security

<br>