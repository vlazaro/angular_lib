# CSS Modules: Scope Locals & Extend

[![Build Status](https://travis-ci.org/css-modules/postcss-modules-scope.svg?branch=master)](https://travis-ci.org/css-modules/postcss-modules-scope)

Transforms:

```css
:local(.continueButton) {
  color: green;
}
```

into:

```css
:export {
  continueButton: __buttons_continueButton_djd347adcxz9;
}
.__buttons_continueButton_djd347adcxz9 {
  color: green;
}
```

so it doesn't pollute CSS global scope and can be simply used in JS like so:

```js
import styles from './buttons.css'
elem.innerHTML = `<button class="${styles.continueButton}">Continue</button>`
```

## Extensions

Since we're exporting class names, there's no reason to export only one. This can give us some really useful reuse of styles:

```css
.globalButtonStyle {
  background: white;
  border: 1px solid;
  border-radius: 0.25rem;
}
.globalButtonStyle:hover {
  box-shadow: 0 0 4px -2px;
}
:local(.continueButton) {
  composes: globalButtonStyle;
  color: green;
}
```

becomes:

```
.globalButtonStyle {
  background: white;
  border: 1px solid;
  border-radius: 0.25rem;
}
.globalButtonStyle:hover {
  box-shadow: 0 0 4px -2px;
}
:local(.continueButton) {
  extends: globalButtonStyle;
  color: green;
}
```

## Local-by-default & reuse across files

You're looking for [CSS Modules](https://github.com/webpack/css-modules). It spans this plugin as well as a few others, and it's amazing.

## Building

```
npm install
npm build
npm test
```

[![Build Status](https://travis-ci.org/css-modules/postcss-modules-scope.svg?branch=master)](https://travis-ci.org/css-modules/postcss-modules-scope)

* Lines: [![Coverage Status](https://coveralls.io/repos/css-modules/postcss-modules-scope/badge.svg?branch=master)](https://coveralls.io/r/css-modules/postcss-modules-scope?branch=master)
* Statements: [![codecov.io](http://codecov.io/github/css-modules/postcss-modules-scope/coverage.svg?branch=master)](http://codecov.io/github/css-modules/postcss-modules-scope?branch=master)

## Development

- `npm watch` will watch `src` for changes and rebuild
- `npm autotest` will watch `src` and `test` for changes and retest

## License

ISC

## With thanks

- Mark Dalgleish
- Tobias Koppers
- Guy Bedford

---
Glen Maddern, 2015.
