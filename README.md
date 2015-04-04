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

## WordPress

### Menus and navigation

### Standard scripts/styles handles

https://github.com/grappler/wp-standard-handles

### Prefixing and scopes

http://themereview.co/prefix-all-the-things/

### Accessibility

### Directory tree structure

#### Of a theme

#### Of a plugin

## Git

- Commit comments start capitalized and end with a period (as sentences), ie. `Initial commit.`, `Added feature XYZ. Closes issue #42.`.

## Other tools

### Bower

### Composer

### Grunt

---

## TODO

- TOC
- Add [EditorConfig file](http://editorconfig.org/)
- https://www.npmjs.com/package/tinypng-cli and image optimization (somewhere)

Created and maintained by [@primozcigler](https://twitter.com/primozcigler).
