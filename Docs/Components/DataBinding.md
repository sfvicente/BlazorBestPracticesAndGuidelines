# Components | Data Binding

Data-binding is the automatic synchronization of data between models and component views. It defines a mechanism for communication between components and the DOM.
<br>


### Use the `@bind` HTML element attribute with a field, property, or _Razor_ expression value to implement data binding in a component.

_Razor_ components allow for binding model data with view elements. To enable data binding, add the `@bind` HMTL attribute and set the attribute with the field name that
will hold the data:

```csharp
<p>
    <input @bind="message" />The message content is: @message
</p>

@code {
    private string message;
}
```

A property can also be used to implement data binding:

```csharp
<p>
    <input @bind="Message" />The message content is: @Message
</p>

@code {
    private string Message { get; set; }
}
```

The content of the fields is copied from the view elements when the control loses focus.
<br>