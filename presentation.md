class: center, middle

.large-image[![Leaflet](./images/gon.png)]
# Gon - yes or no?

???

- who knows?

---

class: middle

# Info

- [Gon on Github](https://github.com/gazay/gon)
- [Gon on RubyGems](https://rubygems.org/gems/gon/versions/6.0.1)
- *"If you need to send some data to your js files and you don't want to do this with long way trough views and parsing - use this force!"*
- [RailsCast 2012](http://railscasts.com/episodes/324-passing-data-to-javascript)
- First release: May 8, 2011
- Last release: July 28, 2015 [6.0.1]

???

- inject data directly into js form rails controller

---

class: middle

# Background

- in 2011 the most popular JsvaScript framework **jQuery**
- **Ruby on Rails** version between 2.3 and 3.0
- **Backbone.js** first release: October 13, 2010
- **AngularJS** first release: October 20, 2010
- **Ember.js** first release: 8 December 2011

???

- Problem of **Speed of initial load**

---

class: middle

# Advantages

- easy and simple
- fast to implementation
- data fast in JavaScript
- without data attributes
- without injection directly to view

---

class: middle

# Disadvantages

- using of gone data
- shared JavaScript files/views
- strong dependences between Rails controller and JavaScript view
- hard to test
- refactoring problem

???

- how we know if we still using gon variable
- how we know what should be set for shared js file, which gon parameters

---

class: middle

# Ideal example

```ruby
def index
  gon.products = Product.limit(10)
  # or
  gon.rabl "app/views/products/index.json.rabl", as: "products"
end
```

---

class: middle

### Life example

```ruby
# before_filters

def index
  (...) # prepare data
  set_permissions
  set_gon_metadata
  gon.company_id = @company.try(:id)
  gon.user = @user
  gon.customers = @customers if is_history?
  gon.months = (1..12).to_a.map { |m| { ... } }
  gon.current_year = Date.current.year
  gon.current_user = current_user.as_json(...)
  gon.companies = @companies.map { |c| { ... } }
  gon.products = @companies.map(&:products).flatten.as_json(...)
  gon.items = logged_items.map { |c| { ... } }
  gon.user_id = @user.try(:id)
  gon.user_type = current_user.user_type
  gon.all_my_tasks = is_true?(params[:all_my_tasks])
  gon.employ_id = @search_params[:employ_id]
  respond
end

def respond
  respond_to do |format|
    format.html { gon.rabl template: 'template_name', as: 'logged_tasks' }
    format.json { render 'app/views/logged_tasks/index.json.rabl' }
  end
end
```

---

class: middle, inverse

# Bibliography

- [Popular JavaScript frameworks 2011](http://www.webappers.com/infographics/javascript-frameworks-jquery.html)
- [Ruby on Rails](https://rubygems.org/gems/rails/versions/4.2.6)
- [Backbone.js](https://en.wikipedia.org/wiki/Backbone.js)
- [AngularJS](https://en.wikipedia.org/wiki/AngularJS)
- [Ember.js](https://en.wikipedia.org/wiki/Ember.js)

---

class: middle, center, contact

.small-image[![Womanonrails](./images/womanonrails.png)]
### Agnieszka Matysek
[@womanonrails](https://twitter.com/womanonrails)

amatysek&#064;fractalsoft&#046;org


