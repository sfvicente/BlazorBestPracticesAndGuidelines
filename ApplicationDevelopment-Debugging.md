# Application Development | Debugging
<br>

**To view more detailed information on exceptions that occur within your application, enable `DetailedErrors`**

Add the code below to your _Startup.cs_ to see more details about exceptions happening in your application:

```
services.AddServerSideBlazor()
     .AddCircuitOptions(o =>
     {
         o.DetailedErrors = true;
     });
```
<br><br>
