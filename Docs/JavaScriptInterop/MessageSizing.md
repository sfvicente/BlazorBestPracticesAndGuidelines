# Javascript Interop | Message Sizing

When performing interop calls within a _Blazor WebAssembly_ application, there is no limit to the size of message payload being sent or received. However, in _Blazor Server_, calls are
restricted to the default 32Kb defined by SignalR. Attempting to transfer content bigger than the allowed payload size will result in an error.
<br>

