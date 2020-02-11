# JavaScript Interop | General
<br>

# JavaScript Interop | General
<br>

**Inject the `JSRuntime` object into a component to execute JSInterop calls within the component.**

Inject the IJSRuntime abstraction into the Razor component using the `inject` keywork.

```
 @page "/"
 @inject IJSRuntime jsRuntime

 <h1 id="title" >Hello, world!</h1>
```
<br><br>


**Inject the `IJSRuntime` abstraction into a class to execute JSInterop calls from within the class.**

Inject the `IJSRuntime` abstraction into a class via constructor injection.

```
TODO: Example
```
<br><br>


**Wrap JavaScript interop calls within `try-catch` statements.**
ToDo: Add description

```
ToDo: Example
```
<br><br>

**Place custom JavaScript code at the bottom of the __Host.cshtml_ file, just below the script section that includes the Blazor code**

```
<script src="_framework/blazor.server.js"></script>
<script>
        window.MyMethods =
        {
            myMethod1: function (element) {
                window.alert(element.id);
            }
        };
</script>
```

<br/><br/>