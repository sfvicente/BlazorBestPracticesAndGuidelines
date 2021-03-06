# Components | User Interface
<br>


### Use the `FocusAsync()` method of `ElementReference` to set the UI focus to an element.

When required, the focus can be set on a UI element programmatically by using the `FocusAsync` method of on `ElementReference`. The `ElementReference` struct represents a
reference to a rendered element.

The following code displays how to set the UI focus on an element.

```csharp
<button @onclick="() => textInput.FocusAsync()">Set focus</button>
<input @ref="textInput"/>
```

Applies To: .NET 5
<br>


### To play or manage a video, use _JSInterop_ to invoke the methods of the HTML5 `video` element.

If you want to play a video from a _Blazor_ application, you will need to write the interop code.
You can bind the `src` from the component but to play (or perform other functions) it is required to call the methods of the `video` element such as `load()` and `play()`. You can do that using _Javascript_ inside _Blazor_.

```charp
@page "/video"

<video>
	<source id="video" src="@videoSource" type="video/mp4">
</video>

code {
	string videoSource;

	// TODO: Add remaining code	
}
```

```javascript
window.playVideo = function(url) {
	var video = document.getElementById('video');

	video.load();
	video.play();
}
```

Additional Tags: JavaScript Interop
<br>


### To access the browser functions `alert()` , `prompt()` and `confirm()`` use JS Interop.

Currently, there isn't a Blazor implementation of the browser functions `alert()` , `prompt()` and `confirm()`. You need to inject the `JSRuntime` object and use _Interop_.

```csharp
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



