# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

```bash
rails g component Button label href theme
```

```ruby
# application_component.rb
class ApplicationComponent << ViewComponent::Base
    include Rails.application.routes.url_helpers
    include Devise::Controllers::Helpers

    def helpers
        ActionController::Base.helpers
    end
end

# button_component.rb
class ButtonComponent << ApplicationComponent 
    def initialize(label: nil, href:, theme:) 
        @label = label
        @href = href
        @theme = theme
    end

    def button_theme
        case @theme
            when :primary
                "btn btn-primary"
            when :secondary 
                "btn btn-secondary"
            else
                "btn btn-primary"
            end
        end
    end

    def render?
        user_signed_in?
    end
end

```

```erb
<% link_to @href, class: button_theme do %>
    <%= @label.present? ? @label : content %>
<% end %>
```

```bash
rails g component nav/container
rials g component nav/item title active href
rails g component logo path
```

```ruby
class Nav::ContainerComponen
    renders_one :logo, LogoComponent,
    renders_many :items, Nav::ItemComponent
end
```