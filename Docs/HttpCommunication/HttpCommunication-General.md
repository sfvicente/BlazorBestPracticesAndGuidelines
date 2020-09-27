# HTTP Communication | General
<br>


## `HttpClient` service

The `HttpClient` service sends HTTP requests and receives HTTP responses from a resource identified by a URI.
<br>


### Do not configure dependency injection for the `HttpClient` service in _Blazor_ _WebAssembly_ applications.

When you create a _Blazor_ _WebAssembly_ application, an HTTP client is automatically configured and injected into the application.
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
<br>


### Use  `GetJsonAsync`  to send HTTP GET requests to a server.

The HttpClient method `GetJsonAsync`  sends an HTTP GET request and parses the JSON response body to create an object.

```csharp
@code {  
        ...       
}  
``` 
<br>


### Use  `PostJsonAsync`  to send HTTP POST requests to a server.

The `HttpClient` method `PostJsonAsync`  sends an HTTP POST request, including JSON-encoded content, and parses the JSON response body to create an object.

```csharp
@code {  
        ...       
}  
``` 
<br>


### Use  `PutJsonAsync`  to send HTTP PUT requests to a server.

The `HttpClient` method `PutJsonAsync`  sends an HTTP PUT request, including JSON-encoded content.

```csharp
@code {  
        ...       
}  
``` 
<br>


### Use  `DeleteAsync`  to send HTTP DELETE requests to a server.

The `HttpClient` method `DeleteAsync`  send a DELETE request to the specified Uri as an asynchronous operation.

```csharp
@code {  
        ...       
}  
``` 
<br>


### Use `SendAsync` and `HttpRequestMessage` to customize requests.

If there is a need to specify the request URI, include specific HTTP headers or use HTTP methods that are not GET, POST, PUT or DELETE. Use `HttpRequestMessage` to configure the message and `SendAsync` to perform communication.

```csharp
TODO: Example
```
<br>