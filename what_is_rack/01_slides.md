!SLIDE bullets incremental

# What is Rack?

* Servers
* Proxies (Middleware)
* Endpoints

!SLIDE small

# Endpoint

    @@@ ruby
    class Rack::Simple::Endpoint
      def call(env)
        [
          200, 
          {
            "Content-Type"=>"text/plain",
            "Content-Length"=>"14",
          },
          "Hello ScotRUG!"
        ]
      end
    end

!SLIDE

# Middleware

    @@@ ruby
    class Rack::Simple::Middleware
      def initialize(app)
        @app = app
      end
      
      def call(env)
        @app.call(env)
      end
    end

!SLIDE code small

    @@@ ruby
    class Rack::Simple::Middleware
      def initialize(app, *args, &block)
        @app = app
      end

      def call(env)
        @env = env
        # Incoming
        status, headers, content = @app.call(@env)
        # Outgoing
        return [status, headers, content]
      end
    end

!SLIDE small

    @@@ ruby
    class TootEverywhere
      def initialize(app)
        @app = app
      end

      def call(env)
        @env = env
        if i_should_toot?
          return a_big_toot
        end
        @app.call @env
      end

      private

      #...

    end

    # http://github.com/bkerley/tooter
    # config.load_paths << "#{config.root}/app/middleware"