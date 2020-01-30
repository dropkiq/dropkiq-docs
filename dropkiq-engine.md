# 🧠 Dropkiq Engine

&nbsp;

The Dropkiq Engine is a javascript library that is the brains of Dropkiq. It is capable of understanding your application's Liquid schema, the context, and the current document the user is typing and making intelligent suggestions.

The Dropkiq Engine can be run anywhere Javascript can be executed. The Dropkiq Engine is paired with a UI so that it can be run in any frontend using any technology.

* [Dropkiq Engine NPM](https://www.npmjs.com/package/dropkiq)

The Dropkiq Engine has a basic version that can be used free of charge. A Pro version license key can be purchased to unlock all features. Visit http://dropkiq.com to learn more.

## Features

* ~111 KB at time of writing (Version 1.0.29)
* Works in any environment in which Javascript can be executed
* Tested in all major browsers (Firefox, Chrome, Safari, and IE)

## Responsibilities

* Parse and understand provided schema, context, and scope objects
* Parse and understand Liquid document
* Determine when a suggestion can be made by analyzing the cursor position
* Return a list of suggestions that can be rendered by the UI

## Installation

Dropkiq Engine is hosted on NPM and can be installed via: npm, yarn, ZIP file, or CDN

**For npm or Yarn:**

```
$ npm install dropkiq
```

or

```
$ yarn add dropkiq
```

Then, access the DropkiqEngine class via require:

```
const { DropkiqEngine } = require('dropkiq')
```

**For ZIP or CDN:**

Add Javascript

```
<script src="https://unpkg.com/dropkiq@1.0.29/dist/dropkiq-engine.min.js">
```

## Usage

* **text** The text document the user is working on
* **cursorIndex** The index of the cursor within the document
* **element** The HTML Textarea, input, or contenteditable element
* **schema** A Javascript object describing your application's Liquid Schema
* **context** A Javascript object describing data available to the current document
* **scope** A Javascript object with test (preview) data
* **licenseKey** Purchased from http://dropkiq.com to unlock the Pro version

&nbsp;

```
// Initialize the Dropkiq Engine
var dropkiqEngine = new DropkiqEngine(text, cursorIndex, schema, context, scope, licenseKey);

// Update the Dropkiq Engine with new text and cursor Position
var result = dropkiqEngine.update(text, cursorIndex);
```

&nbsp;

See [https://codepen.io/akdarrah/pen/yLydVKq](https://codepen.io/akdarrah/pen/yLydVKq) for example.
