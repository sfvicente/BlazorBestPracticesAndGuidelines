# Security

**Always use HTTPS  to protect information in transit** 
[Blazor Server]

SignalR is the mechanism used for communication between a client and the server. A Blazor Server application normally uses the transport that SignalR negotiates, which is typically WebSockets.
A Blazor Server application doesn't ensure the integrity and confidentiality of the data sent between the server and the client, so HTTPS is required.
Blazor Server uses SignalR for communication between the client and the server. Blazor Server normally uses the transport that SignalR negotiates, which is typically WebSockets.

Blazor Server application doesn't ensure the integrity and confidentiality of the data sent between the server and the client, so HTTPS is needed to ensure Always use HTTPS.
<br><br>


**Use *Content Security Policy (CSP)* and  `X-Frame-Options`  header to protect an app from rendering inside of an  `<iframe>`**

```
ToDo: Example
```

<br><br>


**Avoid using user input as part of the navigation call arguments.***

```
ToDo: Example
```

<br><br>


**Validate arguments to ensure that the target is allowed by the app.***

```
ToDo: Example
```

<br><br>


**When rendering links as part of an application, if possible, use relative links.***

```
ToDo: Example
```

<br><br>

**When rendering links as part of an application, validate that absolute link destinations are valid before including them in a page.***

```
ToDo: Example
```

<br><br>