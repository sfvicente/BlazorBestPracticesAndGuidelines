# Application Development | Deployment
<br>

### When deploying a Blazor Server application to IIS, enable both WebSockets and Sticky sessions with Application Request Routing.

TODO: Description
<br>

### When deploying Blazor Server application to an Azure App Service, enable WebSockets and ARR Affinity.

TODO: Description

Turning on ARR Affinity in the App Service will enable sticky sessions. This means that a user will always be routed to the same host machine. The downside of sticky sessions is that the performance might be lower than if this mechanism wasn't enabled.
<br>

