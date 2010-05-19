!SLIDE center

# Underneath

![Zoidberg Naked!](futurama_zoidberg_empty_shell.jpeg)

!SLIDE code smaller

    @@@ ruby
    def build_app(app)
      middleware[options[:environment]].reverse_each do |middleware|
        if middleware.respond_to?(:call)
          middleware = middleware.call(self)
        end
        next unless middleware
        klass = middleware.shift
        app = klass.new(app, *middleware)
      end
      app
    end

!SLIDE code smaller

    @@@ ruby
    def build_app(app)
      middleware[options[:environment]].reverse_each do |middleware|
        # if middleware.respond_to?(:call)
        #   middleware = middleware.call(self)
        # end
        # next unless middleware
        klass = middleware.shift
        app = klass.new(app, *middleware)
      end
      app
    end

