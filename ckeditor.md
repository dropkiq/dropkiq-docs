# ✒️ CKEditor

&nbsp;

The Dropkiq UI library works out of the box with [CKEditor](https://ckeditor.com/).

## Installation

1. Install CKEditor using their [official documentation](https://ckeditor.com/docs/ckeditor4/latest/guide/dev_installation.html).

2. Install Dropkiq UI following the [official documentation](dropkiq-ui.md).

3. Initialize Dropkiq UI with a reference to CKEditor.

```javascript
var editor = CKEDITOR.replace('dropkiq-example');
var dropkiqUI;

editor.on('instanceReady', function(event){
  var window  = editor.window.$;
  var iframe  = window.frameElement;
  var element = window.document.getElementsByTagName("body")[0];

  dropkiqUI = new DropkiqUI(element, schema, context, scope, "", {iframe: iframe});
});

editor.on( 'key', function(evt) {
  // Enter key
  if (evt.data.keyCode === 13 && dropkiqUI.menuMode) {
    evt.cancel();
  }
});
```

&nbsp;

See example code in the [Dropkiq UI Repository](https://github.com/akdarrah/dropkiq-ui/blob/master/demo/ckeditor.html) or view the [live demo.](https://app.dropkiq.com/demos/ckeditor)
