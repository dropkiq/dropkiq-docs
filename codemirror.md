# 🐒 CodeMirror

&nbsp;

The Dropkiq UI library works out of the box with [CodeMirror](https://codemirror.net/).

## Installation

1. Install CodeMirror using their [official documentation](https://codemirror.net/doc/manual.html).

2. Install Dropkiq UI following the [official documentation](dropkiq-ui.md).

3. Initialize Dropkiq UI with a reference to your CodeMirror Editor.

```javascript
var textarea = document.getElementById('dropkiq-example');
var editor = CodeMirror.fromTextArea(textarea, {
  lineNumbers: true
});
new DropkiqUI(editor, schema, context, scope, "");
```

&nbsp;

See example code in the [Dropkiq UI Repository](https://github.com/akdarrah/dropkiq-ui/blob/master/demo/codemirror.html) or view the [live demo.](https://app.dropkiq.com/demos/codemirror)
