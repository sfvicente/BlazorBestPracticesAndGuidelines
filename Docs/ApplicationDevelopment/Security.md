# Security


## HTTPS

Hypertext transfer protocol secure (HTTPS) is the secure version of the HTTP protocol. HTTP is the main protocol used to exchange data between a web browser and a website. Unlike HTTP, HTTPS
is encrypted to provide a secure transfer of data.
<br>


**Always use HTTPS  to protect information in transit** 
[Blazor Server]

SignalR is the mechanism used for communication between a client and the server. A Blazor Server application normally uses the transport that SignalR negotiates, which is typically WebSockets.
A Blazor Server application doesn't ensure the integrity and confidentiality of the data sent between the server and the client, so HTTPS is required.
Blazor Server uses SignalR for communication between the client and the server. Blazor Server normally uses the transport that SignalR negotiates, which is typically WebSockets.

Blazor Server application doesn't ensure the integrity and confidentiality of the data sent between the server and the client, so HTTPS is needed to ensure Always use HTTPS.
<br><br>


**Use *Content Security Policy (CSP)* and  `X-Frame-Options` header to protect an app from rendering inside of an `<iframe>`**

```
ToDo: Example
```
<br><br>


