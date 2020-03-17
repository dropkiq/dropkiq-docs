# 📦 Froala WYSIWYG Editor

&nbsp;

The Dropkiq UI library works out of the box with the Froala WYSIWYG Editor.

## Installation

1. Install Froala using their [official documentation](https://froala.com/wysiwyg-editor/docs/overview/).

2. Install Dropkiq UI following the [official documentation](dropkiq-ui.md).

3. Initialize Dropkiq UI when Froala is initialized.

```javascript
new FroalaEditor('#dropkiq-example', {
  events: {
    initialized: function() {
      var editor = this;

      // Initialize the Standard DropkiqUI for demo elements
      // https://www.npmjs.com/package/dropkiq-ui
      var dropkiqUI = new DropkiqUI(editor.el, schema, context, scope, "");

      editor.events.on('keydown', function(e) {
        if (e.which == FroalaEditor.KEYCODE.ENTER && dropkiqUI.menuMode) {
          return false;
        }
      }, true);
    }
  }
})
```
&nbsp;

## Iframes

Dropkiq is also able to support WYSIWYG editors that use iframes.

Many WYSIWYG editors use iframes to avoid any collisions between the main page content and the content within the WYSIWYG editor. Here is an example of how Froala can be used with Dropkiq with the iframe mode enabled.

```javascript
new FroalaEditor('#dropkiq-iframe-example', {
  iframe: true,
  events: {
    initialized: function() {
      var editor = this;
      var iframe = document.getElementsByClassName("fr-iframe")[0];

      // Initialize the Standard DropkiqUI for demo elements
      // https://www.npmjs.com/package/dropkiq-ui
      var dropkiqUI = new DropkiqUI(editor.el, schema, context, scope, gon.licenseKey, {iframe: iframe});

      editor.events.on('keydown', function(e) {
        if (e.which == FroalaEditor.KEYCODE.ENTER && dropkiqUI.menuMode) {
          return false;
        }
      }, true);
    }
  }
})
```

&nbsp;

See example code in the [Dropkiq UI Repository](https://github.com/akdarrah/dropkiq-ui/blob/master/demo/froala.html) or view the [live demo.](https://app.dropkiq.com/demos/froala)