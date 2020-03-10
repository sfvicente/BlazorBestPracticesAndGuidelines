# Security | Active Directory
<br>


### To change the cookie name when using Azure Active Directory B2C authentication, change the `Cookie.Name` when configuring the `CookieAuthenticationOptions` in the `ConfigureServices` method.

```csharp
services.Configure<CookieAuthenticationOptions>(
	AzureADB2CDefaults.CookieScheme, options =>
	{
		options.Cookie.Name = "MyCookieName";
	});
```
<br>

