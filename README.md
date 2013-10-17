#nested_layout

This project use nested layout

static_page use layout named "user_layout"
product use layout named "product_layout"
user_layout and product_layout use base_layout
##Controller

In `app/controllers/static_pages_controller.rb`

```ruby
class StaticPagesController < ApplicationController                                                                                                                
  layout "user_layout"                                                          
  def index                                                                     
  end                                                                           
end 
```

In `app/controllers/products_controller.rb`

```ruby
class ProductsController < ApplicationController                                                                                                                                                                  
  layout "user_layout"                                                          
  def index                                                                   
  end                                                                           
end
```

##View (important)
1. Create new partial file named "base_layout.html.erb" and put it in `app/views/layout` with content: 
```erb
<!DOCTYPE html>                                                                 
<html lang="ja">                                                                
  <head>                                                                        
    <meta charset="utf-8">                                                      
    <meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">              
    <meta name="viewport" content="width=device-width, initial-scale=1.0">      
    <%= yield(:metatag) if content_for?(:metatag) %>                            
    <title>Nested Layouts</title>                                               
    <%= csrf_meta_tags %>                                                       
                                                                                
  </head>                                                                       
  <body>                                                                        
    <%= content_for?(:content) ? yield(:content) : yield %>                     
    <%= yield(:bottom) if content_for?(:bottom) %>                              
  </body>                                                                       
</html>
```
2. Create 2 index files in `app/views/static_pages` and `app/views/products`
3. Put some text in that 2 file in 

```ruby
<% content_for(:content) do %>
  This is in static page
<% end %>
```
and 

```ruby
  <% content_for(:content) do %>
    This is in product page
  <% end %>
```

Not only `:content`, you can use whatever you defined in `app/views/layout/_base_layout`

This technique is called nested layout. It's can DRY your code in `views` and make your application more reasonable.
