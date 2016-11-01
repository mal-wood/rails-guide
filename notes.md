**SETTING UP REPO AND PUSHING TO GITHUB**<br><br>
1) Create a repo on github without a README<br>
2) Make a directory on local machine with:<br><br>
  `rails new project_name -d postresql -T`<br><br>
3) cd into new directory and:<br><br>
  `git init`<br><br>
4) set remote by using<br><br>
  `git remote add origin https://github.com/somerepo`<br><br> 
5) commit your current files and push your rails skeleton up to github<br><br>

---


---
**AJAX with Rails**

```<form accept-charset="UTF-8" action="/articles" class="new_article" data-remote="true" id="new_article" method="post">
  ...
</form>```

NOTE the **data-remote="true"**!! Now, the form will be submitted by Ajax rather than by the browser's normal submit mechanism.

You probably don't want to just sit there with a filled out `<form>`, though. You probably want to do something upon a successful submission. To do that, bind to the ajax:success event. On failure, use ajax:error. Check it out:
```
$(document).ready ->
  $("#new_article").on("ajax:success", (e, data, status, xhr) ->
    $("#new_article").append xhr.responseText
  ).on "ajax:error", (e, xhr, status, error) ->
    $("#new_article").append "<p>ERROR</p>"
```

Turbolinks magic - ajaxifys all of your links

In `main.js` file: 

```
$(document).on("turbolinks:load", function(){
  alert("Hello world!");
  $('#test-button').on("click", function(event){
    event.preventDefault();
    alert("clicked");
    
    $.ajax({
    method: 'get',
    url: '/cookie'
    }).done(function(response){
      alert(response)
    })
  })
});

```
`get '/cookie', to: "application#cookie"`
^ make custom route 

In application controller: 
```def cookie
    render "hello, it worked!!"
  end```

GEMS to include that Hunter mentioned:
awesome_print<br>
better_errors
binding_of_caller

To include bootstrap: 
- gem bootstrap-sass

- between jQuery and jQuery_ujs

- in main.scss
@import "bootstrap sprockets"
@import "bootstrap" 

---
**CUSTOM ROUTES**

```
Rails.application.routes.draw do 
  #set the controller and action to go to upon to visiting "/"
  #the format is controller#action
  root 'cities#index'
  
  resources :cities, only: :index do 
    resources :parks, except: :destroy do
      resources :reviews
      end
    end 
  end 
```
