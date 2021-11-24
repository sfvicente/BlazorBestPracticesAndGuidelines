# Components | User Interface
<br>


### Use the `FocusAsync()` method of `ElementReference` to set the UI focus to an element.

When required, the focus can be set on a UI element programmatically by using the `FocusAsync` method of on `ElementReference`. The `ElementReference` struct represents a
reference to a rendered element.

The following code displays how to set the UI focus on an element.

```cs
<button @onclick="() => textInput.FocusAsync()">Set focus</button>
<input @ref="textInput"/>
```

Applies To: .NET 5
<br>


### To access the browser functions `alert()` , `prompt()` and `confirm()`` use JS Interop.

Currently, there isn't a Blazor implementation of the browser functions `alert()` , `prompt()` and `confirm()`. You need to inject the `JSRuntime` object and use _Interop_.

```cs
@inject IJSRuntime JsRuntime;
...

@code
{
	...
    bool confirmed = await JsRuntime.InvokeAsync<bool>("confirm", "Are you sure?");
    ...
}
```

Additional Tags: JavaScript Interop
<br>



