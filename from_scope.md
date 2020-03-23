# 🔭 From Scope

&nbsp;

Creating and maintaining Schema and Context data structures is the preferred way to use Dropkiq to unlock all features. However, there may be times when your data is not well defined or may constantly be changing. In this scenario, it may not be ideal or even possible to provide the Schema and Context data objects. Dropkiq is still able to be used in these cases by classifying your data for you on the fly with a given Scope data object.

## Dropkiq Engine Example

Take a look at the following code to see an example of how you can initialize Dropkiq Engine without providing a Schema or Context object. The `DropkiqEngineFromScope` class automatically classifies the provided Scope data and builds these objects for you on the fly.

```javascript
// Test data referred to as the "Scope" object
var scope = {
  email_subject: "Try Dropkiq Today!",
  email_body: "Work faster with a smarter editor. Write complex Liquid statements with ease. Dropkiq Autocompletion gives your users the confidence they need to write their statements correctly the first time.",
  email_from: "Adam Darrah <adam@dropkiq.com>",
  email_contact: {
    name: "John Doe",
    email: "john.doe@dropkiq.com",
    age: 30,
    is_minor: false,
    birthdate: Date.parse("March 18, 1990"),
    notes: "Software developer for application that uses liquid, but users don't fully understand how to use it...",
    favorite_website: {
      nickname: "Dropkiq",
      url: "https://www.dropkiq.com/"
    },
    visited_websites: [
      {nickname: "Dropkiq Ruby Gem", url: "https://github.com/akdarrah/dropkiq-gem"},
      {nickname: "Dropkiq UI", url: "https://github.com/akdarrah/dropkiq-ui"}
    ]
  }
};

var licenseKey = "";
var dropkiqEngineFromScope = new DropkiqEngineFromScope("", 0, scope, licenseKey);
var dropkiqEngine = dropkiqEngineFromScope.dropkiqEngine();

console.log("Generate Schema:", dropkiqEngineFromScope.schema);
console.log("Generate Context:", dropkiqEngineFromScope.context);
```

See a working example on [CodePen](https://codepen.io/akdarrah/pen/JjdmooZ?editors=1010)

## DropkiqUI Example

This feature works almost the exact same way for DropkiqUI as it does for DropkiqEngine. Here is some example code to get you started:

```html
<textarea id="dropkiq-example"></textarea>
```

```javascript
// Test data that is used for the preview feature (optional)
var scope = {
  email_subject: "Try Dropkiq Today!",
  email_body: "Work faster with a smarter editor. Write complex Liquid statements with ease. Dropkiq Autocompletion gives your users the confidence they need to write their statements correctly the first time.",
  email_from: "Adam Darrah <adam@dropkiq.com>",
  email_contact: {
    name: "John Doe",
    email: "john.doe@dropkiq.com",
    age: 30,
    is_minor: false,
    birthdate: Date.parse("March 18, 1990"),
    notes: "Software developer for application that uses liquid, but users don't fully understand how to use it...",
    favorite_website: {
      nickname: "Dropkiq",
      url: "https://www.dropkiq.com/"
    },
    visited_websites: [
      {nickname: "Dropkiq Ruby Gem", url: "https://github.com/akdarrah/dropkiq-gem"},
      {nickname: "Dropkiq UI", url: "https://github.com/akdarrah/dropkiq-ui"}
    ]
  }
};

var licenseKey = "";
new DropkiqUIFromScope(document.getElementById('dropkiq-example'), scope, licenseKey).dropkiqUI();
```

See this code in action on [CodePen](https://codepen.io/akdarrah/pen/GRJYgrK?editors=1010)
