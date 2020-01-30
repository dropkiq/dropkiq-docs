# 🚀 Dropkiq UI

&nbsp;

The Dropkiq UI is a javascript library that brings the Dropkiq Engine to your HTML Textarea, input, or contenteditable fields.

Since many WYSIWYG editors are built on top of contenteditable, there is a chance that DropkiqUI could work without any modification. However, if your WYSISYG doesn't work, feel free to let me know at adam@dropkiq.com.

* [Dropkiq UI Github](https://github.com/akdarrah/dropkiq-ui)
* [Dropkiq UI NPM](https://www.npmjs.com/package/dropkiq-ui)

Dropkiq UI is open source released under the MIT License. In the event that it does not work for your UI needs, it can be used as a starting point for development of a new UI (built using the Dropkiq Engine).

## Features

* ~176 KB at time of writing (Version 1.0.22)
* Works with inputs, textareas, and contenteditable
* Tested in all major browsers (Firefox, Chrome, Safari, and IE)
* No jQuery dependency

## Responsibilities

* Initialize and manage instance of Dropkiq Engine
* Monitor UI events and update Dropkiq Engine with new text and cursor positions
* Take suggestions from the Dropkiq Engine and render it to the screen (draw and position the menu)
* Implement keyboard navigation for menu (Escape, arrow keys, tab, and enter)
* Implement the "Powered by Dropkiq" Promotional banner
* Autocompletion for curly braces ({{}} and {%%})

## Installation

Dropkiq UI is hosted on NPM and can be installed via: npm, yarn, ZIP file, or CDN

**For npm or Yarn:**

```
$ npm install dropkiq-ui
```

or

```
$ yarn add dropkiq-ui
```

Then, access the Dropkiq UI class via require:

```
var { DropkiqUI } = require('dropkiq-ui');
```

In SCSS file:

```
@import 'dropkiq-ui/dist/dropkiq';
```

**For ZIP or CDN:**

Add Javascript

```
<script src="https://unpkg.com/dropkiq-ui@1.0.22/dist/dropkiq.min.js">
```

Add CSS

```
<link rel="stylesheet" type="text/css" href="https://unpkg.com/dropkiq-ui@1.0.22/dist/dropkiq.css">
```

## Usage

* **element** The HTML Textarea, input, or contenteditable element
* **schema** A Javascript object describing your application's Liquid Schema
* **context** A Javascript object describing data available to the current document
* **scope** A Javascript object with test (preview) data
* **licenseKey** Purchased from http://dropkiq.com to unlock the Pro version

&nbsp;

```
new window.DropkiqUI(element, schema, context, scope, licenseKey);
```

&nbsp;

See [https://codepen.io/akdarrah/pen/gObNaMo](https://codepen.io/akdarrah/pen/gObNaMo) for example.
