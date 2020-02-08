# HTTP Communication | CORS
<br>

**When using endpoint routing, configure CORS middleware to execute between the calls to `UseRouting` and `UseEndpoints`.**

Using the wrong configuration sequence will cause the middleware to stop functioning correctly.

```  
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
	...
	app.UseRouting();
	app.UseCors();
	app.UseEndpoints(endpoints =>
	{
		endpoints.MapControllers();
	});
	...
}
``` 
<br><br>


**Do not specify `AllowAnyOrigin` and `AllowCredentials` simultaneously when configuring CORS middleware.**

Using both `AllowAnyOrigin` and `AllowCredentials` is an insecure configuration and can result in cross-site request forgery.

```
TODO: Sample code
```

The CORS service returns an invalid CORS response when an app is configured with both methods.
<br><br>