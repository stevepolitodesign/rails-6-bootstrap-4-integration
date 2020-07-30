1. `rails new rails-bootstrap`
2. `yarn add bootstrap jquery popper.js`
3. Add jQuery and Popper.js plugins

```js
// config/webpack/environment.js
const { environment } = require('@rails/webpacker')
const webpack = require('webpack')

environment.plugins.prepend(
    'Provide',
    new webpack.ProvidePlugin({
      $: 'jquery',
      jQuery: 'jquery',
      jquery: 'jquery',
      'window.jQuery': 'jquery',
      Popper: ['popper.js', 'default'],
    })
)

module.exports = environment
```

> A big problem I ran into was how to correctly import Bootstrap's styles. I intially created `app/javascript/packs/application.scss` and imported the styles in that file. However, that seemed to break my build in a way that made it so `app/javascript/packs/application.js` never compiled. Next, I renamed `app/assets/stylesheets/application.css` to `app/assets/stylesheets/application.scss`, and  imported the styles into that file. That worked, but it meant that the Asset Pipeline was resposnible for my styles. This isn't necesarily a bad thing, but I wanted Webpacker to be responsible for all of my front-end code.    

4. `mkdir app/javascript/stylesheets`
5. `touch app/javascript/stylesheets/application.scss`
6. Import Bootstrap Styles

```scss
// app/javascript/stylesheets/application.scss
@import '~bootstrap/scss/bootstrap'
``` 

7. Import Bootstrap, load styles, and enable [Tooltips](https://getbootstrap.com/docs/4.5/components/tooltips/#example-enable-tooltips-everywhere) and [Popovers](https://getbootstrap.com/docs/4.5/components/popovers/#example-enable-popovers-everywhere)

```js
// app/javascript/packs/application.js
...
require("bootstrap")
import "../stylesheets/application";
$(function () {
    $('[data-toggle="tooltip"]').tooltip()
    $('[data-toggle="popover"]').popover()
})
```

8. Add [Responsive meta tag](https://getbootstrap.com/docs/4.5/getting-started/introduction/#responsive-meta-tag)

```erb
<%# app/views/layouts/application.html.erb %>
<!DOCTYPE html>
<html>
  <head>
    <title>RailsBootstrap</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <%= yield %>
  </body>
</html>
```
