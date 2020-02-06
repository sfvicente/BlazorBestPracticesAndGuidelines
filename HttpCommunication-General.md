# HTTP Communication | General

### General

**Use  `GetJsonAsync`  to send HTTP GET requests to a server**

The HttpClient method `GetJsonAsync`  sends an HTTP GET request and parses the JSON response body to create an object.

```  
@code {  
        ...       
}  
``` 
<BR>

**Use  `PostJsonAsync`  to send HTTP POST requests to a server**

The `HttpClient` method `PostJsonAsync`  sends an HTTP POST request, including JSON-encoded content, and parses the JSON response body to create an object.

```  
@code {  
        ...       
}  
``` 
<BR>

**Use  `PutJsonAsync`  to send HTTP PUT requests to a server**

The `HttpClient` method `PutJsonAsync`  sends an HTTP PUT request, including JSON-encoded content.

```  
@code {  
        ...       
}  
``` 
<BR>

**Use  `DeleteAsync`  to send HTTP DELETE requests to a server**

The `HttpClient` method `DeleteAsync`  send a DELETE request to the specified Uri as an asynchronous operation.

```  
@code {  
        ...       
}  
``` 
<BR>


**Use `SendAsync` and `HttpRequestMessage` to customize requests**

If there is a need to specify the request URI, include specific HTTP headers or use HTTP methods that are not GET, POST, PUT or DELETE. Use `HttpRequestMessage` to configure the message and `SendAsync` to perform communication.

```
TODO: Example
```
