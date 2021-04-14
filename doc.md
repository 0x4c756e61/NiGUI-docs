# Docs for NIGUI framework
## Disclaimer
This documentation may not be complete, I made it only using the examples located in NiGui/examples/

### Setting up a basic NiGui window

First we obviously import the library

```  
import nigui
```

Then we initialize the app

```
app.init()
```

**Creating a new window**

To create a new window we use the `newWindow()` constructor and we pass it the window name (OPTIONAL).

Please note that a window can only contain only ONE control that will be put in the middle of this same window.

**Setting up our window**

To set width and height of ou window we use the width and height variables from our window object

```
window.width = 600.scaleToDpi
window.height = 400.scaleToDpi
```


We can also specify an icon with the `iconPath` variable of our window object, wich should look smth like this `iconPath = "path/to/logo.png"`
we can use PNG as format for our logo but JPEG should work (I DIDN'T TRYED).

**Adding more content**

As I said early windows can only have **1** control, but containers can have multiple ones.

To create a new container we use an other constructor called `newLayoutContainer()` and we pass to it the layout that we want like `Layout_Vertical` or `Layout_Horizontal`.

We then add our container to the window with `window.add(container)` where container is the variable containing our container and window the one that contain our window object.

**Adding Buttons, text areas and onClick event**

To create a new button we use the `newButton()` constructor and we pass to it the label we want our button to have.

We then add our button to our container

`container.add(button)`

We also have text areas that let us write text inside of it! Same here we create one with the `newTextArea()` and we add it to our container with `container.add(textArea)`

If we want our button to add a line to our text area when we click it we use the `button.onClick` event handler. This should look something like this

```
button.onClick = proc(event: ClickEvent) =
  textArea.addLine("Button 1 clicked, message box opened.")
  window.alert("This is a simple message box.")
  textArea.addLine("Message box closed.")
```

**Showing our window and running the app**
To show our window we can use the built-in `window.show()` procedure and the `app.run()` to run main loop of the app

## Detecting when we close the window
To detect when the window get closed we can use the onCloseClick event handler:

```
window.onCloseClick = proc(event: CloseClickEvent) =
  case window.msgBox("Do you want to quit?", "Quit?", "Quit", "Minimize", "Cancel")
  of 1: window.dispose()
  of 2: window.minimize()
  else: discard
```

### All controls
**For all controls**

- `.widthMode` - Set the mode of the control's width
	- `WidthMode_Expand`
- `.xAlign` and `.YAlign` - Set alignment mode on the X and Y axis
	+ `XAlign_Center`
	+ `YAlign_Center`
	+ `XAlign_Right`
	+ `YAlign_Right`
	+ `XAlign_Left`
	+ `YAlign_Left`
- `.width` and `.height` - Set the width and height of the control

**Controls and theire properties**

- `newWindow()` - Create a new window with a title
	+ `.alert()` - Create an alert box with a given string
	+ `.msgBox()` - Create a message box with a given description, title, button 1 and 2  (need to be imported with `import nigui/msgbox`)
	+ `.dispose()` - Closes the window
	+ `.minimize()` - Minimizes the window
- `newLayoutContainer()` - Create a container with a custo layout
	- `.frame = newFrame()` - Add a new frame to the container
	
- `newButton()` - Create a button with a given label
- `newTextArea()` - Create a multiline text box
	- `.addLine()` - Add a line to the text area
- `newCheckbox()` - Create a checkbox with a given label
- `newComboBox()` - Create a combobox with multiple options (NEED TO BE A SEQUENCE)
- `newLabel()` - Create a label with a give string
- `newProgressBar()` -Create a progress bar
	- `.value` - Variable that ajust the progress

- `newTextBox()` - Create a text box that can't be edited, content should be a string

### KeyBoard inputs
if we want to accept imputs from the keyboard like `CTRL+Q` we need to use an event handler like this:
```
window.onKeyDown = proc(event: KeyboardEvent) = 
	do_something()
```

To get the event key we use: `$event.key`

To get the unicode: `event.unicode`

To get the charactere: `event.character`

**Check some key is down**

To check if, let's say `CTRL + Q`, is down, we check `Key_Q` with the `isDown()` procedure:

```
if Key_Q.isDown() and Key_ControlL.isDown():
	app.quit()
```

We quit the app with `app.quit()` when *Q* and *CTRL_left* are both down.
