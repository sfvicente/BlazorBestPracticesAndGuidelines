# HTTP Communication | CORS


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

