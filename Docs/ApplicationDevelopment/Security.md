# Application Development | Security
<br>

## HTTPS

Hypertext transfer protocol secure (HTTPS) is the secure version of the HTTP protocol. HTTP is the main protocol used to exchange data between a web browser and a website. Unlike HTTP, HTTPS
is encrypted to provide a secure transfer of data.
<br>


### Always use HTTPS to protect information in transit.

SignalR is the mechanism used for communication between a client and a Blazor Server application. These applications will use the transport that SignalR negotiates, which will
normally be WebSockets.

A Blazor Server application doe not have mechanisms to ensure the integrity and confidentiality of the data exchange between the clients and the server. HTTPS needs to be
configured to provide data integrity and information confidentiality.

Applies To: Blazor Server
<br><br>


## HTTP Headers
<br>


### Use the `Content-Security-Policy` and `X-Frame-Options` headers to protect an application from rendering inside of an `<iframe>`.

todo: complement description

The `X-Frame-Options` HTTP response header can be used to indicate whether a browser should be allowed to render a page in a <frame>, <iframe>, <embed> or <object>. By
ensuring that their content is not embedded into other sites, an application can use this to avoid click-jacking attacks.

```
ToDo: Example
```

<br><br>


