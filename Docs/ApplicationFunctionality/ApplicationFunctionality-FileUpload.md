# Application Functionality | File Upload
<br>


### To upload files to a server in a _Web Assembly_ application, use an API call.

Do not attempt to store files in a server when using a _Blazor WebAssembly_ application. There is no filesystem as the application is running in the browser, not on the server. 

You can save the data by storing it in `LocalStorage`.

TODO: Code Sample

However, if you wanted to send it to a server, you will need an API on the server and then perform a POST of the file to that API.

TODO: Code Sample
<br>


