# Components | Events
<br>

Use the @on{EVENT}:stopPropagation directive attribute to stop event propagation.

```
<input type="text" value="" @onkeypress:preventDefault />
```

<br/><br/>

Use both the @on{EVENT}:stopPropagation directive attribute and with your event handling to stop event propagation but still process your code.

```
<input type="text" value="" @onkeypress="HandleKeyPresses" @onkeypress:preventDefault />
```
<br><br>


**To detect and handle mouse right-click events, use the `MouseEventArgs` property `Button`**
```
<div @onmouseup="HandleMouseUp" >
    div content
</div>

@code {
    void HandleMouseUp(MouseEventArgs args)
    {
        if (args.Button == 2)
            Console.WriteLine("This is a right click");
    }
}
```
<br><br>


**To handle mouse right-click events and not display the browser context menu, use the HTML `oncontextmenu` attribute**
```
<div oncontextmenu="return false;" @onmouseup="HandleMouseUp">
    div content
</div>

@code {
    void HandleMouseUp(MouseEventArgs args)
    {
        if (args.Button == 2)
            Console.WriteLine("This is a right click");
    }
}
```
<br><br>

