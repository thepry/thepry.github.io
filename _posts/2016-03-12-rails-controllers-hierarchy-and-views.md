---
layout: post
title:  "Rails controllers hierarchy and views"
date:   2016-03-12 4:00
categories: rails
permalink: /rails-controllers-hierarchy-and-views
---

Few weeks ago I found [this](http://jeromedalbert.com/how-dhh-organizes-his-rails-controllers/) post explaining how DHH oranizes controllers in his apps. I also found [this](https://habrahabr.ru/post/136461/)(it's in russian) nice post with a nice example of the controllers hierarchy. The main idea is to organize controllers the same way our website works. For example if there're users on our website and users have posts the controllers structure should be:

```ruby
# config/routes.rb
resources :users do
  scope module: :users do
    resoures :posts
  end
end

# app/controllers/users_controller.rb
class UsersController < ApplicationController
  ...
end

# app/controllers/users/posts_controller.rb
module Users
  class PostsController < ApplicationController
    ...
  end
end
```
  
This structure allows us to keep controllers simple and clean, but requires to write some extra code.

# Problem

The problem is that even if we organize our controller's modules the same way our routes are, we don't want to use the same structure for views. We want to avoid adding the `views/users/posts` directory for our views and keep them in `views/posts`. Of course we could just specify the view path explicitly by calling `render` method:

```ruby
# app/controllers/users/posts_controller.rb
module Users
  class PostsController < ApplicationController
    def index
      render 'posts/index'
    end
  end
end
```

And do the same thing for `render` inside our views:

```ruby
# app/views/posts/index.html.slim
- @posts.each do |post|
  = render partial: 'posts/post', locals: { post: post }
```

# Solution

Instead of specifying each view's path, we could add some magic:

```ruby
# app/controllers/users/posts_controller.rb
module Users
  class PostsController < ApplicationController
    before_filter { lookup_context.prefixes << 'posts' }
  end
end

# app/views/posts/index.html.slim
- @posts.each do |post|
  = render partial: 'post', locals: { post: post }
```

That's better! At first Rails will try to find `index` at `views/users/posts` path. If it's not found, it will look into `views/posts`. But can we make it prettier? Maybe add some DSL? Sure!

```ruby
# app/controllers/concerns/views_path.rb
module ViewsPath
  def add_views_path(path)
    before_filter do
      lookup_context.prefixes << path
    end
  end
end

# app/controllers/application_controller.rb
class ApplicationController < ActionController::Base
  extend ViewsPath
  ...
end

# app/controllers/users/posts_controller.rb
module Users
  class PostsController < ApplicationController
    add_views_path :posts
  end
end
```
