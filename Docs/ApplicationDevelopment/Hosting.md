# Application Development | Hosting

Applications built using the _Blazor_ framework can to run either client-side in the browser on a WebAssembly-based .NET runtime (_Blazor WebAssembly_) or server-side in
_ASP.NET Core_ (_Blazor Server_). 
<br>


## Hosting Model Decision
<br>


### Use _Blazor WebAssembly_ if the application requires offline mode support.

If the application must work when no network connectivity, use the _Blazor WebAssembly_ hosting model. _Blazor Server_ does not support offline mode.

// Todo complement description

<br>


### Use _Blazor Server_ if the application runs or contains sensitive code.

// Todo complement description

<br>