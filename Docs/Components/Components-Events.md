# Components | Events
<br>


### Use the @on{EVENT}:stopPropagation directive attribute to stop event propagation.

```csharp
<input type="text" value="" @onkeypress:preventDefault />
```
<br><br>


### Use both the @on{EVENT}:stopPropagation directive attribute and with your event handling to stop event propagation but still process your code.

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


### Avoid using events that produce large amounts of data in _Blazor Server_ applications.

Example of DOM events that can produce excessive data are `oninput` and `onscroll`.

TODO: complement description

TODO: add code samples

Applies to: Blazor Server
Tags: Events, Security

<br>