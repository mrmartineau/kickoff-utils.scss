# @kickoff/utils.scss
> Sass Functions and Mixins for the Kickoff framework

[![npm version](https://badge.fury.io/js/@kickoff/utils.scss.svg)](https://badge.fury.io/js/kickoff-utils.scss)

[![NPM](https://nodei.co/npm/@kickoff/utils.scss.png)](https://nodei.co/npm/@kickoff/utils.scss/)

## Install

```
npm install @kickoff/utils.scss --save
```

## Usage
With scss and the [npm-sass](https://www.npmjs.com/package/npm-sass) or similar importer like [eyeglass](https://github.com/sass-eyeglass/eyeglass).

```scss
@import "kickoff-utils.scss" // with npm-sass
@import "kickoff-utils" // with eyeglass
```

## Functions

### [_colors.scss](/scss/functions/_colors.scss)
> Various color functions

```scss
// With a color palette map like this:
$color-palette: (
  white: (
    base: #ffffff
  ),

  sky: (
    lighter: #f9fafb,
    light: #f4f6f8,
    base: #dfe3e8,
    dark: #c4cdd5
  )
);

// ko-color() function
a {
  color: ko-color(white); // picks the `base` value
  color: ko-color(sky, dark); // picks the `dark` variant
  color: ko-color(sky, lighter); // picks the `lighter` variant
}

// ko-color-tint() function
// Add percentage of white to a color
a {
  background-color: ko-color-tint(blue, 20%);
}

// ko-color-shade() function
// Add percentage of black to a color
a {
  background-color: ko-color-tint(red, 10%);
}
```

### [_get-value.scss](/scss/functions/_get-value.scss)
> Retrieve value from sass map. Often used within the `font-size` mixin. There are a number of utility functions that make use of this function, see the [source file](functions/_get-value.scss)

```scss
// map helper
ko-getValue(mid, $map) // uses a Sass map

// breakpoints helper
ko-bp(mid) // uses the $breakpoints Sass map
```

### [_map-deep-get.scss](/scss/functions/_map-deep-get.scss)
> Retrieve value from deeply nested sass map

```scss
 $grid-configuration: (
   'columns': 12,
   'layouts': (
     'small': 800px,
     'medium': 1000px,
     'large': 1200px,
   ),
 );

 div {
   font-size: ko-map-deep-get($grid-configuration, 'columns');
   width: ko-map-deep-get($grid-configuration, 'layouts', 'medium');
 }
```

### [_modular-scale.scss](/scss/functions/_modular-scale.scss)
> Sizes type using a consistent vertical rythm

```scss
// Used in the kickoff $type sass map variable
ko-modular-scale($font-size-base, -1, $type-scale)
ko-modular-scale($font-size-base, 1, $type-scale)
ko-modular-scale($font-size-base, 3, $type-scale)


// or using this shorthand, we assume that `$font-size-base` & `$type-scale` are already set somewhere (in Kickoff, they are set in the _variables.scss file):
$font-size-base: 20;
$type-scale: 1.4

ko-ms(-1)
ko-ms(1)
ko-ms(3)

// e.g.
a {
	font-size: @include font-size(ko-ms(3));
}
```

### [_multiply.scss](/scss/functions/_multiply.scss)
> Multiply any value

```scss
ko-multiply(15, 2)
ko-multiply($baseline, 1.5)

// e.g.
a {
	margin-bottom: ko-multiply($baseline, 1.5);
}
```

### [_px-to-em.scss](/scss/functions/_px-to-em.scss)
> Convert px em

For a relational value of 12px write ko-em(12) when the parent is 16px
If the parent is another value say 24px write ko-em(12, 24)

Usage:
```scss
font-size : ko-em(12);
font-size : ko-em(12, 24);
```

### [_px-to-rem.scss](/scss/functions/_px-to-rem.scss) -
> Convert px rem

### [_strip-units.scss](/scss/functions/_strip-units.scss)
> Strip units

### [_tint-shade.scss](/scss/functions/_tint-shade.scss)
> Add percentage of white or black to a colour

```scss
// Add percentage of white to a color
background-color: ko-tint(blue, 20%);

// Add percentage of black to a color
background-color: ko-shade(blue, 20%);
```

## Mixins

### [_hidpi.scss](/scss/mixins/_hidpi.scss)
> Hi-dpi media query mixin

```scss
@include ko-hidpi {
	...
}
```

### [_module-naming-helpers.scss](/scss/mixins/_module-naming-helpers.scss)
> Provides consistent class naming through the usage of mixins

See https://gist.github.com/mrmartineau/0cd2010bf265d712bafb for usage

### [_position.scss](/scss/mixins/_position.scss)
> Position shortcut

```scss
@include ko-position(absolute, 10px 20px 30px 10px);
```

### [_responsive-reveal.scss](/scss/mixins/_responsive-reveal.scss)
> Responsive helper classes to show/hide content based on our `$breakpoints` map

```scss
@include ko-rwd-reveal();
```

### [_responsive.scss](/scss/mixins/_responsive.scss)
> Responsive media-queries. **We recommend the use of [include-media](http://include-media.com) for media-queries now.**

```scss
// min-width
// Equivalent to: @media screen and (min-width: 20em) { ... }
@include ko-respond-min(mid) { ... }; // uses the $breakpoints sass-map
@include ko-respond-min(650) { ... }; // converts to px

// max-width
// Equivalent to: @media screen and (max-width: 20em) { ... }
@include ko-respond-min(large) { ... }; // uses the $breakpoints sass-map
@include ko-respond-min(460) { ... }; // converts to px

// min-max-width
// Equivalent to: @media screen and (min-width: 10em) and (max-width: 20em) { ... }
@include ko-respond-min-max(narrow, large) { ... }; // uses the $breakpoints sass-map
@include ko-respond-min-max(460, 900) { ... }; // converts to px
```

### [_units.scss](/scss/mixins/_units.scss)
> Dimension-based mixins

* REM calculation: `@include ko-rem(margin, $font-size-base);`
* REM font-size: `@include ko-font-size(16);`
* REM line-height: `@include ko-line-height(22);`
* EM font-size: `@include ko-font-size-ems(20, 16);`

### [_utility.scss](/scss/mixins/_utility.scss)
> Utility Mixins

* clearfix: `@include ko-clearfix;`
* Text truncation: `@include ko-truncate(100%);`
* and a [bunch more](/scss/mixins/utility.scss)

### [_vertical-centre.scss](/scss/mixins/_vertical-centre.scss)
> Vertically center any element. Needs support for CSS tranforms.

```scss
@include vertical-center;
```
