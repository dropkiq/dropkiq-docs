# 🏎 Using IFrames

&nbsp;

Many WYSIWYG editors, such as [Froala](froala.md), use IFrames to separate the main page content from the editor's content. This prevents any Javascript or CSS from the main page from "leaking" into the editor's content. While you typically wouldn't use an iframe unless you're working with a WYSIWYG editor, it can be helpful to understand how to initialize Dropkiq for any editable textarea embedded within an iframe. This is often an easy way to integrate Dropkiq with *any* WYSIWYG editor. Even if you're the first person to ever attempt the integration!

DropkiqUI supports an option called "iframe", where you must pass a reference to the iframe element. This allows Dropkiq to understand it is working with an element embedded within an iframe and position things correctly.

## Installation

1. Let's assume that you are working with the following HTML:

```html
<iframe id="dropkiq-iframe">
  <html>
    <body>
      <textarea id="iframe-example"></textarea>
    </body>
  </html>
</iframe>
```

2. Javascript to initialize Dropkiq UI for the textarea

```javascript
document.getElementById("dropkiq-iframe").onload = function(){
  var iframe    = this;
  var iframeDoc = iframe.contentWindow.document;
  var element   = iframeDoc.getElementById('iframe-example');

  new window.DropkiqUI(element, schema, context, scope, gon.licenseKey, {iframe: iframe});
}
```

&nbsp;

You can take a look at the [Froala](froala.md) example to understand how you would use this capability in practice to integrate with a WYSIWYG editor. A live demo of an iframe integration can be [viewed on CodePen](https://codepen.io/akdarrah/pen/vYOrExX?editors=1010)
