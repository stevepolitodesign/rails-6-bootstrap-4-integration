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
