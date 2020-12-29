# Security | General
<br>

### To retrieve the list of claims from a JWT token, parse the payload content using a JSON deserializer.

```csharp
public static IEnumerable<Claim> ParseClaimsFromJwt(string jwt)
	{
		var payload = jwt.Split('.')[1];
		var jsonBytes = ParseBase64WithoutPadding(payload);
		var keyValuePairs = JsonSerializer.Deserialize<Dictionary<string, object>>(jsonBytes);

		return keyValuePairs.Select(kvp => new Claim(kvp.Key, kvp.Value.ToString()));
	}

	private static byte[] ParseBase64WithoutPadding(string base64)
	{
		switch (base64.Length % 4)
		{
			case 2: base64 += "=="; break;
			case 3: base64 += "="; break;
		}

		return Convert.FromBase64String(base64);
	}
```
<small>Reference: [https://stackoverflow.com/questions/60404612/parse-jwt-token-to-get-the-payload-content-only-without-external-library-in-c-sh](https://stackoverflow.com/questions/60404612/parse-jwt-token-to-get-the-payload-content-only-without-external-library-in-c-sh)</small>
<br>


## Shared State
<br>


### Do not share state between apps on the same server using singleton services unless the services have been specifically designed for it.

Blazor server applications run and use server memory. When multiple applications are hosted on the same server, those applications share the same process. Blazor initiates
a circuit for each application session which has its own DI container scope. While this makes scoped services unique per Blazor session, singleton services do not share this
behavior.

Without careful design considerations, sharing state with singleton services can introduce security vulnerabilities, such as leaking user state across circuits.

Applies to: Blazor Server
<br>


### Do not use `IHttpContextAccessor` within Blazor apps.

As _Blazor_ applications do not run within the context of the _ASP.NET Core_ pipeline, using the `IHttpContextAccessor` is a security risk. The `HttpContext` is not
guaranteed to be available within the `IHttpContextAccessor`. There is also no guaranteed that it is holding the context that started the Blazor application.

todo: add code sample.

<br>


### To make request state available to an application, pass data through parameters to the root component in the initial rendering of the application.

The `IHttpContextAccessor` ´should not be used within Blazor apps. To make request state available to an application

Create a class to hold all the data needed:

todo: code example

In the initial rendering of the application, populate the class with data using the `HttpContext` information available at that point:

todo: code example

Pass the information to the _Blazor_ application as a parameter to the root component:

todo: code example

Use the data within the application directly or through a scoped service.

todo: code example


Additional Tags: HTTP Context
<br>