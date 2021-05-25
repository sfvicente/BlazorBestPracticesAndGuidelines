# Application Functionality | File Upload
<br>


### Use the `InputFile` component for handling file uploads or reading browser file data into an application.

The `InputFile` component renders as an HTML input of type `file`. By default, the user can select single files, or if you add the "multiple" attribute then the user can supply
multiple files at once. When one or more files is selected by the user, the `InputFile` component fires an `OnChange` event and passes in an `InputFileChangeEventArgs` that provides
access to the selected file list and details about each file.

```csharp
<InputFile OnChange="OnInputFileChange" multiple />

<div class="image-list">
    @foreach (var imageDataUrl in imageDataUrls)
    {
        <img src="@imageDataUrl" />
    }
</div>

@code {
    IList<string> imageDataUrls = new List<string>();

    async Task OnInputFileChange(InputFileChangeEventArgs e)
    {
        var imageFiles = e.GetMultipleFiles();

        var format = "image/png";
        foreach (var imageFile in imageFiles)
        {
            var resizedImageFile = await imageFile.RequestImageFileAsync(format, 100, 100);
            var buffer = new byte[resizedImageFile.Size];
            await resizedImageFile.OpenReadStream().ReadAsync(buffer);
            var imageDataUrl = $"data:{format};base64,{Convert.ToBase64String(buffer)}";
            imageDataUrls.Add(imageDataUrl);
        }
    }
}
```

To read data from a user-selected file, you call `OpenReadStream` on the file and read from the returned stream. In a Blazor WebAssembly app, the data is streamed directly into
your .NET code within the browser. In a Blazor Server app, the file data is streamed to your .NET code on the server as you read from the stream.

Applies To: Blazor WebAssembly, Blazor Server

References:
    ASP.NET Core updates in .NET 5 Release Candidate 1
	ASP.NET Blog, 14 Sep 2020
	https://devblogs.microsoft.com/aspnet/asp-net-core-updates-in-net-5-release-candidate-1/
<br><br>


### To upload files to a server in a _Web Assembly_ application, use an API call.

Do not attempt to store files in a server when using a _Blazor WebAssembly_ application. There is no filesystem as the application is running in the browser, not on the server. 

You can save the data by storing it in `LocalStorage`.

TODO: Code Sample

However, if you wanted to send it to a server, you will need an API on the server and then perform a POST of the file to that API.

TODO: Code Sample
<br>


