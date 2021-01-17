# Application Development | Hosting

Applications built using the _Blazor_ framework can to run either client-side in the browser on a WebAssembly-based .NET runtime (_Blazor WebAssembly_) or server-side in
_ASP.NET Core_ (_Blazor Server_). 
<br>


### Optimize _Blazor Server_ applications to minimize UI latency by reducing network latency and memory usage.

todo: add description

Applies To: Blazor Server
Additional Tags: Performance
<br>


### Limit application memory usage to improve application latency.

When memory consumption increases within an application, it can trigger an increase in garbage collection or paging of memory to disk. Both of these mechanisms impact the application
performance which leads to UI latency.

todo: complement description

Applies To: Blazor Server
Additional Tags: Performance
<br>


## Hosting Model Decision
<br>


### User _Blazor WebAssembly_ if the application requires offline mode support.

If the application must work when no network connectivity, use the _Blazor WebAssembly_ hosting model. _Blazor Server_ does not support offline mode.

// Todo complement description

<br>


### Use _Blazor Server_ if the application runs or contains sensitive code.

// Todo complement description

<br>