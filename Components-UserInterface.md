# Components | User Interface
<br>


### To set the focus to a text box element, use _JSInterop_ to invoke the `focus()` _JavaScript_ function.

At the moment, the only way to achieve this functionality is by using _JSInterop_.

```csharp
<input type="text" @ref="myref"/>

@code {
	private ElementReference myref;
    [Inject] IJSRuntime JSRuntime { get; set; }

    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
	    if (firstRender)
        {
	        await JSRuntime.InvokeVoidAsync("exampleJsFunctions.focusElement", myref);
        }
   }
}
```
```javascript
<script>
    window.exampleJsFunctions =
    {
        focusElement: function(element) {
           element.focus();
        }
	};
</script>
```
<br><br>


