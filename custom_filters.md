# ⛽️ Custom Filters

&nbsp;

DropkiqUI allows you to register additional custom filters your company may use. When you register a new filter, you add a Javascript implementation for client side rendering along with additional data required to allow Dropkiq to use the custom filter as a suggestion.

## Dropkiq Engine Example

Once you have your DropkiqEngine instance, you can use the "registerFilter" function to add a new Liquid Filter. Here is a description of the arguments:

1. **Name:** The first argument "fire" is the name for the new filter.
2. **Function:** Add a Javascript implementation of your filter for client side rendering.
3. **Template:** This is what will be inserted when the user clicks on a suggestion.
4. **Selection:** The fourth argument is always an array with two numbers. This represents the indices of the characters to auto-select once the suggestion is inserted. In this case, when the user selects the fire filter suggestion, we want it to automatically select the "3".
5. **Hint:** The last argument is a hint to provide the user (This is the only optional argument).

```javascript
var dropkiqEngine = new DropkiqEngine("", 0, schema, context, scope, licenseKey);

dropkiqEngine.registerFilter('fire', function(str, count){
  return str + '🔥'.repeat(count);
}, "fire: 3", [6,7], "add n 🔥-emojis to the end of your string");
```

See this example [on CodePen.](https://codepen.io/akdarrah/pen/LYVawML?editors=1010)

## DropkiqUI Example

This works exactly the same way with an instance of DropkiqUI. Here is some example code:

```javascript
var dropkiqUI = new DropkiqUIFromScope(document.getElementById('dropkiq-example'), scope, "").dropkiqUI();

dropkiqUI.registerFilter('fire', function(str, count){
  return str + '🔥'.repeat(count);
}, "fire: 3", [6,7], "add n 🔥-emojis to the end of your string");
```

See this example [on CodePen.](https://codepen.io/akdarrah/pen/GRJLKow?editors=1010)

## Custom Filter with No Arguments

You may be asking to yourself how the "Selection" argument works if you have a custom filer that has no arguments. The answers is simple. Make the index numbers the same value so that there is no selection and the cursor goes to the end of the filter. Here is an example:

```javascript
var dropkiqUI = new DropkiqUIFromScope(document.getElementById('dropkiq-example'), scope, "").dropkiqUI();

dropkiqUI.registerFilter('fire', function(str, count){
  return str + '🔥'.repeat(count);
}, "fire: 3", [6,7], "add n 🔥-emojis to the end of your string");
```

If your filter has multiple arguments, we recommend you make the first argument be selected by default. This will allow the user to easily change the value before continuing to the second argument.
