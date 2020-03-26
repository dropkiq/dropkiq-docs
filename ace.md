# 🛩 Ace Code Editor

&nbsp;

The Dropkiq UI library works out of the box with [Ace Code Editor](https://ace.c9.io/).

## Installation

1. Install Ace using their [official documentation](https://ace.c9.io/#nav=embedding).

2. Install Dropkiq UI following the [official documentation](dropkiq-ui.md).

3. Initialize Dropkiq UI with a reference to your Ace Editor.

```javascript
var editor = ace.edit("dropkiq-example");
var dropkiqUI = new DropkiqUI(editor, schema, context, scope, "");

var keyboardHandler = {
  handleKeyboard: function(editor, index, name, keyCode){
    if(dropkiqUI.menuIsOpen() && [27, 38, 40, 9, 13].includes(keyCode)){
      return {command:"null", passEvent:false};
    }
  }
}
editor.keyBinding.addKeyboardHandler(keyboardHandler);
```

&nbsp;

See example code in the [Dropkiq UI Repository](https://github.com/akdarrah/dropkiq-ui/blob/master/demo/ace.html) or view the [live demo.](https://app.dropkiq.com/demos/ace)
