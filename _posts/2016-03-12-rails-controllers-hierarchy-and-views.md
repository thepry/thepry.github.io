---
layout: post
title:  "Rails controller hierarchy and views"
date:   2016-03-12 12:00
categories: rails
permalink: /rails-controllers-hierarchy-and-views
---

Few weeks ago i found [this](http://jeromedalbert.com/how-dhh-organizes-his-rails-controllers/) post explaining how DHH oranizes controllers in his apps. I also found [this](https://habrahabr.ru/post/136461/) great post (it's in russian) with a nice example of controllers hierarchy. The main idea is to organize controllers the same way our website works. For example if there're users on our website and users have posts the controllers structure should be:

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
  
This structure allows us to keep controllers simple and clean, but requires to write extra code.

### Problems

The problem is that even if we organize our controller's modules the same way our routes are, we don't want to use the same structure for views. Often we want to use the same views in multiple controllers. We want to avoid adding the `views/users/posts` directory for our views and want to keep them in `views/posts`. Of course it's not a problem, we just need to specify view path explicitly by calling `render` method:

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

And do the same thing for `render` inside our views. But that's not a rails way. There's no magic, we like so much :)

```ruby
# app/controllers/users/posts_controller.rb
module Users
  class PostsController < ApplicationController
    before_filter { lookup_context.prefixes << 'posts' }
  end
end
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

# app/controllers/users/posts_controller.rb
module Users
  class PostsController < ApplicationController
    extend ViewsPath
    add_views_path :posts
  end
end
```
