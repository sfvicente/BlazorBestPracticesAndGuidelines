# Components | Media
<br>


### To play or manage a video, use _JSInterop_ to invoke the methods of the HTML5 `video` element.

If you want to play a video from a _Blazor_ application, you will need to write the interop code.
You can bind the `src` from the component but to play (or perform other functions) it is required to call the methods of the `video` element such as `load()` and `play()`. You can do that using _Javascript_ inside _Blazor_.

```cs
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
