# Mobvious

Mobvious detects whether your app / website is being accessed by a phone, or by a tablet,
or by a personal computer.

## Key Features

* **It's easy to get running.** Just a Rack middleware with almost no config. (See
  section Get Started below.)

* **It supports multiple strategies for detection.** If you don't like the default ones,
  you can easily write your own. (See section Detection Strategies below.)

* **Works with Rails, Sinatra, or whatever.** Does not depend on any application
  framework, uses just Rack.
  

## Get Started

1.  **Include Mobvious in your Gemfile**: `gem 'mobvious'`

2.  **Tell your app to use Mobvious::Manager as Rack middleware.**  
    If you use Rails, simply add `config.middleware.use Mobvious::Manager` into your
    `config/application.rb` file.

3.  **Tell Mobvious which strategies it should use.**  
    A good place to put this code for Rails is an initializer – create a file
    `config/initializers/mobvious.rb` and put this in:

        Mobvious.configure do
          strategies = [ Mobvious::Strategies::MobileESP.new ]
        end

4.  **Done! From now on, device type is detected for each request.**  
    The information is
    in a Rack environment variable `env['mobvious.device_type']`, this variable will
    have a value of `:desktop` or `:mobile` depending on the device type that issued
    the request. In Rails, you can access it via `request.env['mobvious.device_type']`.

*This is just a very basic way of setting up Mobvious. If you want to detect
tablets separately, or let the user manually switch between interface versions of your
app, or do some funnier stuff, see sections Detection Process and Detection Strategies.*

## Detection Process

Mobvious uses an array of strategies to detect the device type.
Strategies are evaluated in order of appearance in the array. Each strategy may or
may not be successful in determining the device type. The result of the first successful
strategy is used. If no strategy is successful, the implicit device type is used
(defaults to `:desktop`, but this is configurable via `default_device_type` attribute
in the `configure` block).


## Detection Strategies

### MobileESP

### URL

### Cookie

### Writing Your Own