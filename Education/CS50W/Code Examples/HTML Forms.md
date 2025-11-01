The HTML `<form>` element is used with user input, usually to send to a server for processing.

The `<form>` element is a container for different types of input elements, all of which can be seen [on w3schools HTML Form Elements](https://www.w3schools.com/html/html_form_elements.asp) page, but the most used one is `<input>`.


Input Attributes
- `type=` 
- `id=`
- `name=`
- `value=`


An `<input>` element depends on it's `type=` attribute for how it can be displayed;
- `<input type="text">` displays a single-line text input field
- `<input type="radio">` displays a radio button, for selecting one of multiple choices
- `<input type="checkbox">` displays a checkbox, for selecting multiple simultaneous choices
- `<input type="submit">` displays a submit button for submitting the form
- `<input type="button">` displays a clickable button
- `<input type="hidden">` lets you include information that cannot be modified by users when a form is submitted 


All of the `type=` attributes that can be used with `<input>` can be seen on [w3schools HTML Input Types](https://www.w3schools.com/html/html_form_input_types.asp) page

#### Using Labels with HTML Forms
Here is an example of a form with one input field for text:
```html
<form>  
  <label for="fname">First name:</label><br>  
  <input type="text" id="fname" name="fname"><br>
</form>
```
The `<label>` tag binds the text "First name:" with the `<input>` tag that has the `id="fname"` by using `for="fname"` as an identifier. When the user clicks on the text contained within the form, it will automatically focus the input field and allow the user to start typing as if they had just clicked on the input field.

This feature of automatically focusing the field associated with the label tag is especially useful when it comes to using radio buttons or checkboxes, since it highlights those input fields, making it easier to select choices.


The `name=` attribute that is used in forms provides a key that identifies data provided by whatever was passed into the input fields.

Google search queries are formatted like this:  `field1=value1&field2=value2&field3=value3...`, and each `field=value` is really just `input tag's identifier described by 'name=' = information tied to that input field, that the user inputted` 

If multiple input elements all have the same `name=` attribute (which is common for checkboxes appaerently), then they are all sent with the same name. But that is useful because when the server interprets this, it can group related information together in something like an array.


The `value=` attribute is used to be sent as the default value connected to an input's key, if that input gets selected by the user. If it isn't selected, then that key/value pair doesn't get sent in the first place.

If `value=` is used in an input field that can be changed by the user, like a text field, then that information is sent instead of what the default value is.