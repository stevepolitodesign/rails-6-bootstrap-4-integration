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
