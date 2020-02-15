# 🧠 Suggestion Filter

&nbsp;

The `suggestionFilter` option gives you complete control over Dropkiq suggestion results. This can be used to modify the suggestions to fit your application's needs. Common use cases could be: adding additional suggestions, removing unwanted suggestions, modifying suggestions, or even adding server side rendering for previews!

Here is a quick example showing how to modify Preview messages!

## Example: Modify Preview Messages

The `suggestionFilter` function receives the list of suggestions to be rendered by DropkiqUI. In this example, we'll simply override the suggestion's preview with a new message.

``` javascript
var suggestionFilter = function(suggestions){
  suggestions.forEach(function(suggestion){
    suggestion['preview'] = "Overridden from suggestionFilter";
  });
}
```

Then, this function is passed to your `DropkiqUI` instance:

``` javascript
var options = {
  suggestionFilter: suggestionFilter
}
new DropkiqUI(document.getElementById('text-area-example'), schema, context, scope, gon.licenseKey, options);
```

See a live example on [Codepen](https://codepen.io/akdarrah/pen/bGdpVYJ).

## Example: Server Side Rendering

This example gets a little more complex because we are dealing with an ajax request (an asynchronous promise). Here is what our JS might look like for this example:

``` javascript
var dropkiqUI;

var suggestionFilter = function(suggestions){
  var requestParams = {toRender: {}}

  suggestions.forEach(function(suggestion){
    // (Optional) Remove the preview rendered Client side
    // suggestion['preview'] = null;

    // Add each suggestion to params to be sent to the Server
    // for server-side preview rendering
    requestParams.toRender[suggestion.name] = suggestion.template;
  });

  // Send request to render Liquid server side
  $.ajax({
    type    : "POST",
    url     : "/demos/render",
    data    : requestParams,
    success : function(response){
      Object.keys(response).forEach(function(name){
        var suggestion = suggestions.find(function(suggestion){
          return suggestion.name === name;
        })

        suggestion['preview'] = response[name];
      })

      // Tell the UI to update after changing the data
      dropkiqUI.renderSuggestions();
    }
  });
}

dropkiqUI = new DropkiqUI(document.getElementById('text-area-example'), schema, context, scope, gon.licenseKey, options);
```

Here's an example of what your Ruby on Rails controller code may look like to handle this request:

``` ruby
class ExampleController < ApplicationController
  def render_liquid
    @scope = {
      "email_subject" => "(From Server) Try Dropkiq Today!",
      "email_body"    => "(From Server) Work faster with a smarter editor. Write complex Liquid statements with ease. Dropkiq Autocompletion gives your users the confidence they need to write their statements correctly the first time.",
      "email_from"    => "(From Server) Adam Darrah <adam@dropkiq.com>",
      "email_contact" => {
        "name"      => "(From Server) John Doe",
        "email"     => "(From Server) john.doe@dropkiq.com",
        "age"       => 30,
        "is_minor"  => false,
        "birthdate" => Time.parse("March 18, 1990"),
        "notes"     => "(From Server) Software developer for application that uses liquid, but users don't fully understand how to use it...",
        "favorite_website" => {
          "nickname" => "(From Server) Dropkiq",
          "url"      => "(From Server) https://www.dropkiq.com/"
        },
        "visited_websites" => [
          {
            "nickname" => "(From Server) Dropkiq Ruby Gem",
            "url"      => "(From Server) https://github.com/akdarrah/dropkiq-gem"
          },
          {
            "nickname" => "(From Server) Dropkiq UI",
            "url"      => "(From Server) https://github.com/akdarrah/dropkiq-ui"
          }
        ]
      }
    }

    response = {}
    params[:toRender].each do |name, template|
      response[name] = Liquid::Template.parse(template).render(@scope)
    end

    render json: response, status: :ok
  end
end
```

You can see this code in action with the "Server Side Rendering" example of the [official demo](https://app.dropkiq.com/demo).
