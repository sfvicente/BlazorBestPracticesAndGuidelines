# HTTP Communication | General
<br>


## `HttpClient` Service

The `HttpClient` service sends HTTP requests and receives HTTP responses from a resource identified by a URI.
<br>


### Do not configure dependency injection for the `HttpClient` service in _Blazor_ _WebAssembly_ applications.

When you create a _Blazor WebAssembly_ application, an HTTP client is automatically configured and injected into the application. Therefore, there is no need to
configure dependency injection for the 'HttpCLient'.

Applies To: Blazor WebAssembly
<br>


### To perform HTTP communication in a _Blazor Server_ application, provide an `HttpClient` to the application using the `HttpClient` factory infrastructure.

A _Blazor Server_ application doesn't include an `HttpClient` service by default. To use the `HttpClient` service, call the `AddHttpClient()` on the service configuration:

```csharp
public class Startup
{
	public Startup(IConfiguration configuration) 
	{
		Configuration = configuration;
	}

	public IConfiguration Configuration { get; }

	public void ConfigureServices(IServiceCollection services)
	{
		services.AddHttpClient();
		...
```

Applies To: Blazor Server
<br>


### To perform HTTP communication requests, inject an `HttpClient` instance using the `@inject` directive.

An `HttpClient` can be requested using dependency injection (DI).

todo: complement description

```csharp
@using System.Net.Http
@inject HttpClient Http

@code {
    private CartProduct[] cartProducts;

    protected override async Task OnInitializedAsync() => 
         cartProducts = await Http.GetFromJsonAsync<CartProduct[]>("api/CartProducts");
}
```

<br>


## HTTP Request Methods

HTTP requests are actions to be performed on a resource identified by a given Uri.
<br>


### Use `GetJsonAsync` to send HTTP GET requests to a server.

The HttpClient method `GetJsonAsync` sends an HTTP GET request and parses the JSON response body to create an object.

```csharp
@code {  
        ...       
}  
```

And the corresponding API operation:

```csharp
[HttpGet("{id}")]
public async Task<ActionResult<Message>> GetMessage(int id)
{
    var message = await _context.Messages.FirstOrDefaultAsync(m => m.Id == id);

    if (message == null)
    {
        return NotFound();
    }

    return message;
}
```
<br>


### Use `PostJsonAsync` to send HTTP POST requests to a server.

The `HttpClient` method `PostJsonAsync` sends an HTTP POST request, including JSON-encoded content, and parses the JSON response body to create an object.

```csharp
@code {  
        ...       
}  
```

And the corresponding API operation:

```csharp
[HttpPost]
public async Task<ActionResult<Message>> PostMessage(Message message)
{
    _context.Messages.Add(message);
    await _context.SaveChangesAsync();

    return CreatedAtAction("GetMessage", new { id = message.Id }, message);
}
```
<br>


### Use `PutJsonAsync` to send HTTP PUT requests to a server.

The `HttpClient` method `PutJsonAsync` sends an HTTP PUT request, including JSON-encoded content.

```csharp
@code {  
        ...       
}  
```

And the corresponding API operation:

```csharp
[HttpPut("{id}")]
public async Task<IActionResult> PutMessage(Message message)
{
    ...

    var existingMessage = _context.Messages.Where(m => m.Id == message.Id).FirstOrDefault<Message>();

    if (existingMessage != null)
    {
        existingMessage.Content = message.Content;
        existingMessage.From = message.From;

        await _context.SaveChangesAsync();

        return Ok();
    }

    return NotFound();
}
```
<br>


### Use `DeleteAsync` to send HTTP DELETE requests to a server.

The `HttpClient` method `DeleteAsync` send a DELETE request to the specified Uri as an asynchronous operation.

```csharp
@page "/messages/delete"

@inject HttpClient Http
@inject NavigationManager Navigate

...

@code {
    protected async Task Delete()
    {
        await Http.DeleteAsync("api/messages/" + Convert.ToInt32(messageId));

        ...

        Navigate.NavigateTo("/messages");
    }
}
``` 

And the corresponding Web API operation:

```csharp
[HttpDelete("{id}")]
public async Task<ActionResult<Messages>> DeleteMessage(int id)
{
    var message = await _context.Messages.FindAsync(id);

    if (message == null)
    {
        return NotFound();
    }

    _context.Messages.Remove(message);
    await _context.SaveChangesAsync();

    return message;
}
```
<br>


## Request Customization
<br>


### Use `SendAsync` and `HttpRequestMessage` to customize requests.

Requests can be customized if there is a need to specify the request URI, include specific HTTP headers or use HTTP methods that are
not GET, POST, PUT or DELETE. Use the `HttpRequestMessage` class to configure the message and `SendAsync` to perform communication.

```csharp
@using System.Net.Http
@using System.Net.Http.Headers
@using System.Net.Http.Json
@inject HttpClient Http

...

@code {

    private async Task GetCartItems()
    {
        var requestMessage = new HttpRequestMessage()
        {
            Method = new HttpMethod("GET"),
            RequestUri = new Uri("https://localhost/api/getCartItems")
        };

        requestMessage.Content.Headers.TryAddWithoutValidation("x-custom-header", "value");

        var response = await Http.SendAsync(requestMessage);

        ...
        }
    }

}
```
<br>


### Use the `SetBrowserResponseStreamingEnabled` extension method on the request to enable support for response streaming.

<An HTTP response is typically buffered in a _Blazor WebAssembly_ app to enable support for sync reads on the response content.>

```csharp
@page "/streaming-example"
@inject HttpClient HttpClient

<button @onclick="MakeStreamingRequest">Make Streaming Request</button>

@code {
    private async Task MakeStreamingRequest()
    {
        var request = new HttpRequestMessage(HttpMethod.Get, "https://api.example.com/large-data");
        
        // Enable response streaming for this request
        request.SetBrowserResponseStreamingEnabled(true);

        using (var response = await HttpClient.SendAsync(request, HttpCompletionOption.ResponseHeadersRead))
        {
            if (response.IsSuccessStatusCode)
            {
                // Read the response stream incrementally
                using (var stream = await response.Content.ReadAsStreamAsync())
                {
                    byte[] buffer = new byte[4096];
                    int bytesRead;
                    
                    // Process the stream data in chunks
                    do
                    {
                        bytesRead = await stream.ReadAsync(buffer, 0, buffer.Length);
                        // Process the received data here (e.g., append to UI)
                        Console.WriteLine($"Received {bytesRead} bytes");
                    }
                    while (bytesRead > 0);
                }
            }
            else
            {
                Console.WriteLine($"Request failed with status code: {response.StatusCode}");
            }
        }
    }
}
```
<br>


### Use the `SetBrowserRequestCredentials` extension method to include credentials in a cross-origin request.

todo: add description

```csharp
@page "/cross-origin-example"
@inject HttpClient HttpClient

<button @onclick="MakeCrossOriginRequest">Make Cross-Origin Request</button>

@code {
    private async Task MakeCrossOriginRequest()
    {
        var request = new HttpRequestMessage(HttpMethod.Get, "https://api.example.com/data");
        
        // Include credentials in the cross-origin request
        request.SetBrowserRequestCredentials(BrowserRequestCredentials.Include);

        using (var response = await HttpClient.SendAsync(request))
        {
            if (response.IsSuccessStatusCode)
            {
                var content = await response.Content.ReadAsStringAsync();
                Console.WriteLine($"Response content: {content}");
            }
            else
            {
                Console.WriteLine($"Request failed with status code: {response.StatusCode}");
            }
        }
    }
}
```

<sub>Applies to: Blazor WebAssembly</sub>
<br>
<sub>Additional tags: `security` `authentication`</sub>
<br>