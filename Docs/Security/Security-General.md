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

