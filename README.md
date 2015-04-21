# Coding Rules and Guides

These are code style rules, guides and examples of ProteusThemes development team. Everyone contributing code to ProteusThemes should be familiar with the contents of this document.

## Code style guides and naming conventions

### HTML

Adhere to the [Code Guide](http://codeguide.co/#html) and additionally:

- Use real tabs instead of spaces for indentation.
- Use BEM for naming HTML classes where appropriate, see the [CSS](#css) below.
- Things like language attributes and charset should be left to the CMS, and not hardcoded - WordPress in our case.

### CSS

Word CSS is used for simplicity and general understanding. We actually write SASS, more specifically SCSS syntax.

Adhere to the [Code Guide](http://codeguide.co/#css) and additionally:

- Use real tabs instead of spaces for indentation.
- Don't use shorthand hex values. Good: `#ffffff`, wrong: `#fff`.
- When possible follow the [BEM naming](https://css-tricks.com/bem-101/) of HTML classes.
- Each BEM component has its own `_component-name.scss` file, in folder `components/` relative to main CSS file.
- Main SCSS file in the theme has a filename `style.scss` (for the WordPress themes compatibility).
- Classes representing state should start with `.is-*`, example: `.is-focus`, `.is-hover`.
- The main CSS file in WP theme must include a class [`.screen-reader-text`](https://make.wordpress.org/accessibility/2015/02/09/hiding-text-for-screen-readers-with-wordpress-core/).
- Other related links:
  - [WordPress CSS Coding Standards](https://make.wordpress.org/core/handbook/coding-standards/css/)
  - [CSS Guidelines](http://cssguidelin.es/) - very comprehensive guide by [Harry Roberts](https://twitter.com/csswizardry).

### JavaScript

### PHP

As we write 99% PHP for WP, follow their [PHP Coding Standards](https://make.wordpress.org/core/handbook/coding-standards/php/). The only difference is the [brace style](https://make.wordpress.org/core/handbook/coding-standards/php/#brace-style) - mind additional new line after closing `}`:

```php
if ( condition ) {
  action1();
  action2();
}
else if ( condition2 && condition3 ) {
  action3();
  action4();
}
else {
  defaultaction();
}
```

## WordPress

### Menus and navigation

We use [WordPress navigation] (https://codex.wordpress.org/Function_Reference/wp_nav_menu) with the [Bootstrap] (http://getbootstrap.com/components/#navbar) elements (for collapsed mobile navbar).

- Add semantic `<nav>` element around the WordPress code for menu.
- Add arrays for wp_nav_menu: 
```
'theme_location' => 'main-menu',
'container' => false,
'menu_class' => 'main-navigation'
```
Change `main` with different name if there is more menus.

### Standard scripts/styles handles

Follow rules from the [WP Standard Handles](https://github.com/grappler/wp-standard-handles) guide. See the mentioned link for:

- How to name script/style handles.
- How to properly register/enqueue Google Fonts.
- How to name image size handles added via [`add_image_size`](https://codex.wordpress.org/Function_Reference/add_image_size).

Additionally, follow these rules when naming handles:

- The handles should be prefixed (if they are not in the list of the standard handles).
- Name the handles for the main scripts/styles like this:
  - `<prefix>-admin-script` for the main JS file used in wp-admin
  - `<prefix>-admin-style` for the main CSS file used in wp-admin
  - `<prefix>-script` for the main JS file used on frontend  
  - `<prefix>-style` for the main CSS file used on frontend
- All the custom scripts/styles should have the same version as the plugin, defined dynamically (so there is no need to update the handles once the plugin/theme is updated to the newer version). Use like this:

  ```php
wp_enqueue_style( '<prefix>-admin', <PREFIX>_URL . 'assets/stylesheets/admin.css', array( 'dep1', 'dep2' ), <PREFIX>_VERSION );
```

### Prefixing and scopes

http://themereview.co/prefix-all-the-things/

### Accessibility

- Hide [screen reader text](https://make.wordpress.org/accessibility/2015/02/09/hiding-text-for-screen-readers-with-wordpress-core/) with this code:

  ```css
  .screen-reader-text {
    clip: rect(1px, 1px, 1px, 1px);
    position: absolute !important;
    height: 1px;
    width: 1px;
    overflow: hidden;
  }
  ```
- All inputs and textareas must have lables.
- Icon fonts (social icons for example) should have fallback text for screen readers.
- Use [ARIA landmark] (https://make.wordpress.org/themes/handbook/review/accessibility/required/#aria-landmark-roles) roles.
- Use `<strong>` and `<em>` instead of `<bold>` and `<i>` (even if screen readers sees them the same - [source] (http://webaim.org/techniques/semanticstructure/)).

#### Navigation Accessibility

- Add `role="navigation"` and `aria-label="<?php _e( 'Name of the Menu', 'textdomain' ); ?>"` on `<nav>`.
- Add `role="menubar"` only on the first `ul` if `ul` is horizontal.
- Add `role="menuitem"` on all `li` element or `role="presentation"` (if there is still bug in validator).
- Add `role="menu"` on al `ul`s width sub-menu.
- Add `aria-haspopup="true"` on `li` with sub-menu.
- Add `aria-expanded="false"` on all `li` elements with sub-menu on default. Change to `aria-expanded="true"` if sub-menu is open.

### Directory tree structure

*TODO*

#### Of a theme

#### Of a plugin

### WP Customizer

- [Improvements in WP 4.0](https://make.wordpress.org/core/2014/07/08/customizer-improvements-in-4-0/): panels, new controls (supporting all HTML5 input types), contextual controls.
- [Improvements in WP 4.1](https://make.wordpress.org/core/2014/11/17/jsunderscore-template-rendered-custom-customizer-controls-in-wordpress-4-1/): registering control types, sending PHP control data to JS, JS/Underscore templating.

## Git

- Commit comments start capitalized and end with a period (as sentences), ie. `Initial commit.`, `Added feature XYZ. Closes issue #42.`.
- [This](https://www.reviewboard.org/docs/codebase/dev/git/clean-commits/) is a guide how the commits history should look like.
- Version names follow [Semantic Versioning](http://semver.org/).

### Git hooks

We use [git hooks](http://git-scm.com/docs/githooks) in order to check the code quality and run some automatic tests. When you make a commit in our projects, the committed PHP files are checked against WordPress standards. By doing this, we ensure that the code quality is of the highest standard.
#### Installation

In order for the git hooks to run smoothly you will need to install and configure some dependencies:

- Install [WordPress Coding Standards for PHP_CodeSniffer](https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards). Follow the instructions on the page and make sure to include the library to the PATH variable of your OS (so the phpcs command will be available globally).
- In your project folder run the command `grunt githooks`. This will configure/apply the git hooks.

## Other tools

### Bower

All 3rd party **frontend** dependencies should be included via [Bower](http://bower.io/), so the repo stays clean and it is easy to update to future versions from comfort of terminal.

In rare occasions the backend dependencides can be included via bower as well, if they don't support Composer packages.

### Composer

All **backend** dependencies should be inluded via [Composer](https://getcomposer.org/), the same resons as for [Bower](#bower).

### Grunt

---

## TODO

- TOC
- Add [EditorConfig file](http://editorconfig.org/)
- https://www.npmjs.com/package/tinypng-cli and image optimization (somewhere)

Created and maintained by [@primozcigler](https://twitter.com/primozcigler).
