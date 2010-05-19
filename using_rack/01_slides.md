!SLIDE bullets incremental

# Using Rack

* Rails
* Sinatra
* `config.ru`

!SLIDE small

# Rails

## `$ rake middleware`

## `config/environment.rb`:

    @@@ ruby
    
    config.middleware.use(new_middleware, args)
    config.middleware.insert_before(existing_middleware, 
                                    new_middleware, 
                                    args)
    config.middleware.swap(middleware_a, middleware_b)
    config.middleware.delete(middleware)

!SLIDE smaller

# Rails

## `config/initializer/fun_stuff.rb`

    @@@ ruby
    
    ActionController::Dispatcher.middleware.use(Rack::Zoidberg, 
                                                args) do 
      # fun stuff goes here!  
      # Rack::Rewrite                                       
    end

!SLIDE small

# Sinatra

    @@@ ruby
    
    use(Rack::Zoidberg, args) do
      # fun stuff goes here!
    end
    
# `config.ru`

    @@@ ruby
    
    use(Rack::Zoidberg, args) do
      # fun stuff goes here!
    end
    
    run Rack::Lobster

!SLIDE bullets incremental

# Finding and Using Rack Stuff

* [`rack-contrib`](http://github.com/rack/rack-contrib)
* [CodeRack](http://coderack.org/)
* [Rubygems](http://rubygems.org/gems?letter=R)

!SLIDE bullets incremental

# Writing your own

* Endpoints go in `app/metal` (Rails only)
* or `lib` (everyone else)
* Middlewares go in `lib`

!SLIDE smaller

# [Directory Conventions for Rack Middleware RubyGems](http://blog.smartlogicsolutions.com/2010/05/13/directory-conventions-for-rack-middleware-rubygems/)

    lib/
    |-- rack/
    |   |-- zoidberg/
    |   |   |-- ...
    |   |   `-- ...
    |   `-- zoidberg.rb
    `-- rack-zoidberg.rb # this one should just require 'rack/zoidberg'
    
## allows:

    @@@ ruby
    
    require 'rack/zoidberg'
    # or
    require 'rack-zoidberg'
    # then
    use Rack::Zoidberg, args

# rack-contrib

!SLIDE bullets incremental

# Convenience Methods

* `@request = Rack::Request.new(env)`
* `@response = Rack::Response.new(body, status, headers)`
