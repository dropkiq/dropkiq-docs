# ⚡️ Ruby on Rails Quick Start

&nbsp;

#### 1. Add the &nbsp; [Dropkiq Ruby Gem](https://github.com/akdarrah/dropkiq-gem) to your application

Add the Gem to your application's `Gemfile`:

```bash
gem 'dropkiq', "~> 0.1.11", git: "https://github.com/akdarrah/dropkiq-gem"
```

Run bundle to install the Gem:

```bash
$ bundle
```

&nbsp;

#### 2. Use the Dropkiq Ruby Gem to generate your application's Dropkiq Schema file

```bash
$ bundle exec rake dropkiq:schema
```

Follow the Gem [instructions](https://github.com/akdarrah/dropkiq-gem#usage) to manually fix any "CHANGEME" entries in your file.

&nbsp;

#### 3. Install the Dropkiq UI Javascript code

[Download](https://app.dropkiq.com/download) Dropkiq UI. This guide will assume that your application uses [Webpacker](https://github.com/rails/webpacker) and we'll install using Yarn.

```bash
$ yarn add dropkiq-ui
```

Then, in `app/javascript/packs/example-bundle.ts`, import `DropkiqUI`:

```javascript
var { DropkiqUI } = require('dropkiq-ui');
window['DropkiqUI'] = DropkiqUI;
```

Import the stylesheets in `app/assets/stylesheets/application.scss`:

```sass
@import 'dropkiq-ui/dist/dropkiq';
```

&nbsp;

#### 4. Import `dropkiq_schema.yaml` to your frontend with the &nbsp; [Gon](https://github.com/gazay/gon) gem

Use the following code to load the `db/dropkiq_schema.yaml` file in your Rails controller:

```ruby
class ExamplesController < ApplicationController
  before_action :load_dropkiq_schema
  # ...

  private

  # ...
  def load_dropkiq_schema
    gon.dropkiq_schema = YAML.load_file("#{Rails.root}/db/dropkiq_schema.yaml")
  end
end
```

&nbsp;

#### 5. Use javascript to initialize the Dropkiq UI in your view:

```javascript
// Load the dropkiq_schema.yaml file (Required)
var schema = gon.dropkiq_schema;

// Declare data the user has for this document (Required)
var context = {
  example: {
    type: "ColumnTypes::HasOne",
    foreign_table_name: "examples"
  },
  name: {
    type: "ColumnTypes::String",
    foreign_table_name: null
  }
}

// Add test data for previewing (Optional)
var scope = {
  name: "Example Name",
  example: {
    // ...
  }
};

// Get a licenseKey from https://dropkiq.com (For Pro Version)
var licenseKey = "";

new window.DropkiqUI(document.getElementById('dropkiq-textarea'), schema, context, scope, licenseKey);
```
