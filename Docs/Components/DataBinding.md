# Components | Data Binding

Data-binding is the automatic synchronization of data between models and component views. It defines a mechanism for communication between components and the DOM.
<br>


### Use the `@bind` HTML element attribute with a field, property, or _Razor_ expression value to implement data binding in a component.

_Razor_ components allow for binding model data with view elements. To enable data binding, add the `@bind` HMTL attribute and set the attribute with the field name that
will hold the data. Take into account that attribute binding is case sensitive.

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

In this case, the content of the fields is copied from the view elements when the control loses focus as binding uses the `onchange` event by default.
<br>


### Use the '@bind:event' HTML element attribute to bind a property or field to other events instead of the default binding event for an element.

The `@bind` attribute uses a pre-configured event to use for data binding. In case of an input field, it binds to the control `onchange` event. To use another event,
we can apply the `@bind:event` attribute with an event parameter instead.

The example below performs data binding on a input field with the `oninput` event:

```csharp
<input @bind="message" @bind:event="oninput" />
The message content is: @message

@code {
    private string message { get; set; }
}
```
<br>


## Formatting
<br>


### Do not use the `@bind:format` HTML element attribute to format strings containing currency or number content.

Using binding to format currencies or number formats is not currently supported.
<br>


