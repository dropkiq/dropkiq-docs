# 🔍 TinyMCE

&nbsp;

The Dropkiq UI library works out of the box with [TinyMCE](https://www.tiny.cloud/).

## Installation

1. Install TinyMCE using their [official documentation](https://www.tiny.cloud/docs/quick-start/).

2. Install Dropkiq UI following the [official documentation](dropkiq-ui.md).

3. Initialize Dropkiq UI with a reference to TinyMCE.

```javascript
tinymce.init({
 selector: '#dropkiq-example',
 setup: function(editor){
   var dropkiqUI;

   editor.on('init', function(e) {
     var iframe  = editor.iframeElement;
     var element = editor.contentDocument.getElementById("tinymce");

     // Initialize the Standard DropkiqUI for demo elements
     // https://www.npmjs.com/package/dropkiq-ui
     dropkiqUI = new DropkiqUI(element, schema, context, scope, gon.licenseKey, {
       iframe: iframe
     });
   });

   editor.on('keydown',function(e) {
     if(e.keyCode == 13 && dropkiqUI.menuIsOpen()){
       return false;
     }
   });
 }
});
```

&nbsp;

See example code in the [Dropkiq UI Repository](https://github.com/akdarrah/dropkiq-ui/blob/master/demo/tinymce.html) or view the [live demo.](https://app.dropkiq.com/demos/tinymce)
