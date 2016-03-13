---
layout: post
title:  "Rails views path gem released"
date:   2016-03-14 0:20
categories: rails
permalink: /rails-views-path-gem
---

# Version 0.1.0

I've created gem which allows to add views paths in controller. I wrote about this problem in my [previous](http://thepry.github.io/rails-controllers-hierarchy-and-views) post.

So just

```ruby
# Gemfile
gem 'rails_views_path'

# app/controllers/users/posts_controller.rb
module Users
  class PostsController < ApplicationController
    add_views_path :posts
  end
end
```
After that for each action Rails will look into `app/views/users/posts/` and if view is not found, into `app/views/posts/`.

