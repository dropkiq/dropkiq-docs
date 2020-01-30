# 🥊 Javascript Quick Start

&nbsp;

**It is recommended that everyone reads this (even if you intend to use Dropkiq in a Ruby on Rails application).**

This guide is intended to help you understand how the DropkiqUI works and can be quickly implemented in your web application (even if you don't use Ruby on Rails).

For this example, we will use a pretend "Email Marketing" application as an example (as used in the [Dropkiq Demo](https://app.dropkiq.com/demo)). In our app, we have a "Contact" and "Website" model.

&nbsp;

#### 1. Install the Dropkiq UI Library in Your Application

Use the [Dropkiq Download](https://app.dropkiq.com/download) page to determine the best way for you to download Dropkiq UI. In this example, we'll use Yarn:

```
$ yarn add dropkiq-ui
```

```
var { DropkiqUI } = require('dropkiq-ui');
```

&nbsp;

#### 2. Declare your Schema (Required)

For Ruby on Rails applications, your Schema can be automatically generated using the [Dropkiq Ruby Gem](https://github.com/akdarrah/dropkiq-gem). However, the Dropkiq Ruby Gem is not required! Your schema can be created in any way that makes sense for your application. The only requirement is that the data must be in the following format:

```
var schema = {
  "[YOUR_TABLE_OR_MODEL_NAME]": {
    "methods": {
      "[METHOD_NAME]": {
        type: "ColumnTypes::[DATA_TYPE]",
        foreign_table_name: "[OPTIONAL_OTHER_TABLE_NAME]",
        hint: "[OPTIONAL_HINT]"
      }
    }
  }
}
```

For our application, let's assume that we have the following `Liquid::Drop` classes:


```
class ContactDrop < Liquid::Drop
  def initialize(contact)
    @contact = contact
  end

  def name
    @contact["name"] # "Adam"
  end

  def email
    @contact["email"] # "adam@dropkiq.com"
  end

  def age
    @contact["age"] # 29
  end

  def is_minor
    @contact["is_minor"] # false
  end

  def birthdate
    @contact["birthdate"] # 1990-03-18 00:00:00 -0500
  end

  def notes
    @contact["notes"] # "Super excited about Dropkiq... 🔥🔥🔥"
  end

  # Could be has_one, belongs_to, or even a method
  # Anything that returns a Website object
  def favorite_website
    @contact["favorite_website"] # #<Website ...>
  end

  # could be a has_many, HABTM, or a method
  # Anything that returns an array of Website object
  def visited_websites
    @contact["visited_websites"] # [#<Website ...>, #<Website ...>, ...]
  end
end
```

```
class WebsiteDrop < Liquid::Drop
  def initialize(website)
    @website = website
  end

  def nickname
    @website["nickname"] # "Dropkiq"
  end

  def url
    @website["url"] # "https://dropkiq.com"
  end
end
```

Since this is only two classes, it is trivial to write the Schema by hand. Keep in mind that "hint" is optional.

```
var schema = {
  contacts: {
    methods: {
      name: {
        type: "ColumnTypes::String",
        foreign_table_name: null,
        hint: "The full name of the contact person"
      },
      email: {
        type: "ColumnTypes::String",
        foreign_table_name: null,
        hint: "The email address of the contact person"
      },
      age: {
        type: "ColumnTypes::Numeric",
        foreign_table_name: null,
        hint: "The computed age of the contact person"
      },
      is_minor: {
        type: "ColumnTypes::Boolean",
        foreign_table_name: null,
        hint: "Is true if the person is less than 18 years old"
      },
      birthdate: {
        type: "ColumnTypes::DateTime",
        foreign_table_name: null,
        hint: "The birthdate of the contact person"
      },
      notes: {
        type: "ColumnTypes::Text",
        foreign_table_name: null,
        hint: "Any notes that are saved in the database"
      },
      favorite_website: {
        type: "ColumnTypes::HasOne",
        foreign_table_name: "websites",
        hint: "The website the person visits most often"
      },
      visited_websites: {
        type: "ColumnTypes::HasMany",
        foreign_table_name: "websites",
        hint: "A list of websites the person has visited"
      }
    }
  },
  websites: {
    methods: {
      nickname: {
        type: "ColumnTypes::String",
        foreign_table_name: null,
        hint: "The nickname of the website"
      },
      url: {
        type: "ColumnTypes::String",
        foreign_table_name: null,
        hint: "The website HTTP URL address"
      }
    }
  }
};
```

&nbsp;

#### 3. Declare the Context (Required)

Your schema object describes how classes are associated within your application for Liquid. Context describes what data the user has at the time of writing the current document. In other words, this should match the data that your application will provide at the time Liquid is actually rendered.

For example, let's say that the user is writing a marketing email within the application. Your context could look something like this:

```
var context = {
  email_subject: {
    type: "ColumnTypes::String",
    foreign_table_name: null,
    hint: "The subject of the email to send"
  },
  email_body: {
    type: "ColumnTypes::Text",
    foreign_table_name: null,
    hint: "The body of the email to send"
  },
  email_from: {
    type: "ColumnTypes::String",
    foreign_table_name: null,
    hint: "The email address the email will be sent from"
  },
  email_contact: {
    type: "ColumnTypes::HasOne",
    foreign_table_name: "contacts",
    hint: "The contact who will receive the email"
  }
};
```

Notice that we are referencing the schema through `foreign_table_name`. Additionally, you can add primitive data to the context that is not defined in the schema.

&nbsp;

#### 4. Declare the Scope (Optional)

The scope data is optional, and provides test data that Dropkiq will render as Previews along side each suggestion. For our example, we can provide an object that looks like this:

```
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
```

&nbsp;

#### 5. Bringing It All Together

Now that we have our `schema`, `context`, and `scope`, we can use this data to bring our DropkiqUI to life! Let's assume that we have the following HTML code in our view:

```
<textarea id="dropkiq-example"></textarea>
```

Our javascript will look like this:

```
var textArea = document.getElementById('dropkiq-example');
var options  = {};
new window.DropkiqUI(textArea, schema, context, scope, "license-key-goes-here", options);
```

See the full example on CodePen: [https://codepen.io/akdarrah/pen/gObNaMo](https://codepen.io/akdarrah/pen/gObNaMo)
