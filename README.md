# Webpack Drupal plugin

A Webpack plugin that bridges Webpack-built assets with Drupal extensions by
generating a php file that returns the webpack-emitted assets as library
definitions to be used in [`hook_library_info_build()`](https://api.drupal.org/apis/hook_library_info_build).

## Dependencies

Imports are automatically mapped to [Webpack externals](https://webpack.js.org/configuration/externals)

### Top-level Core libraries

Special libraries:

| Import                                        | Drupal Library      |
| --------------------------------------------- | ------------------- |
| `import Drupal from 'Drupal'`                 | core/drupal         |
| `import drupalSettings from 'drupalSettings'` | core/drupalSettings |

Otherwise, for all other libraries they will be mapped by
`Drupal/[library/name] → library/name`. For example,
`import Drupal from 'Drupal/core/drupal.debounce'` will automatically register
`core/drupal.debounce` library as a dependency. All library imports will give
the `Drupal` global object.

### Third-party libraries

Third-party imports that exist in Drupal core will also be mapped, according to
their [npm](https://npmjs.com/) package names (as well as the above pattern).

| Import                                               | Drupal Library          |
| ---------------------------------------------------- | ----------------------- |
| `import Backbone from 'backbone'`                    | core/backbone           |
| `import CKEDITOR from 'ckeditor4'`                   | core/ckeditor           |
| `import 'es6-promise/auto'`                          | core/es6-promise        |
| `import jQuery from 'jquery'`                        | core/jquery             |
| `import jQuery from 'jquery-cookie'`                 | core/jquery.cookie      |
| `import jQuery from 'farbtastic'`                    | core/jquery.farbtastic  |
| `import jQuery from 'jquery-form'`                   | core/jquery.form        |
| `import jQuery from 'joyride'`                       | core/jquery.joyride     |
| `import jQuery from 'jquery-once'`                   | core/jquery.once        |
| `import jQuery from 'jquery-ui'`                     | core/jquery.ui.widget   |
| `import jQuery from 'jquery-ui/ui/widget'`           | core/jquery.ui.widget   |
| `import jQuery from 'jquery-ui/ui/widgets/[widget]'` | core/jquery.ui.[widget] |
| `import jQuery from 'jquery-ui/ui/position'`         | core/jquery.ui.position |
| `import Modernizr from 'modernizr'`                  | core/modernizr          |
| `import Popper from '@popperjs/core'`                | core/popperjs           |
| `import Sortable from 'sortablejs'`                  | core/sortable           |
| `import Cookies from 'js-cookie'`                    | core/js-cookie          |

As indicated above, the import will give the appropriate global if it exists.

## Options

Explanation and defaults of options for the plugin are given below.

```js
module.exports = {
  // ...
  plugins: [
    new DrupalPlugin({
      // The filename of the PHP file exported.
      filename: 'assets.php',
    }),
  ],
};
```
