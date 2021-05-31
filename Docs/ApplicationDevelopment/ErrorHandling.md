# Application Development | Error Handling

<br>


### Consider customizing the error handling experience in the `wwwroot/index.html` file.

The `index.html` in the _wwwroot_ folder contains the following code:

```
<div id="blazor-error-ui">
    An unhandled error has occurred.
    <a href="" class="reload">Reload</a>
    <a class="dismiss">🗙</a>
</div>
```

TODO: complement description

Applies To: Blazor WebAssembly
<br><br><br>


### Consider customizing the error handling experience in the `Pages/_Host.cshtml` file.

TODO: complement description

The `_Host.cshtml` in the _Pages_ folder contains the following code:

```
<div id="blazor-error-ui">
    <environment include="Staging,Production">
        An error has occurred. This application may no longer respond until reloaded.
    </environment>
    <environment include="Development">
        An unhandled exception has occurred. See browser dev tools for details.
    </environment>
    <a href="" class="reload">Reload</a>
    <a class="dismiss">🗙</a>
</div>
```

Applies To: Blazor Server
<br>