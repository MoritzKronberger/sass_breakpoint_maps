# Sass Breakpoint Maps

A minimal Sass library for decluttering your media queries using Sass maps and CSS custom properties

## Installation

```bash
npm i sass-breakpoint-maps
```

Import into your Sass file with:

```scss
// your path may be different
@use '../node_modules/sass-breakpoint-maps' as sbpm;
```

## Usage

Define a Sass map containing your project's breakpoints (Both the map and property names can be changed freely):

```scss
$breakpoints: (
  tablet: 1060px,
  mobile: 870px
);
```

Define a Sass map containing the custom properties and their desired values at the breakpoints, as well as a base value (The map name can be changed freely):

```scss
$custom-properties: (
  margin-top: (
    regular: 1rem,
    tablet: 2rem,
    desktop: 3rem
  ),
  padding-top: (
    regular: 2rem,
    desktop: 1rem
  ),
  grid-gap: (
    regular: 7px,
    desktop: 10%
  )
);
```

Call the `create-breakpoints` mixin within your application's `:root` tags:

```scss
:root {
  @include sbpm.create-breakpoints($custom-properties, $breakpoints);
}
```

**Media Queries are set up mobile first by default** (using `min-width`), this can be overridden in the mixin:

```scss
:root {
  @include sbpm.create-breakpoints($custom-properties, $breakpoints, $mobile-first: false);
}
```

`regular` is the default name for the base value, but can be changed when calling the mixin, too:

```scss
$custom-properties: (
  margin-top: (
    m: 1rem,
    l: 2rem,
    s: .5rem
  ),
  padding-top: (
    m: 2rem,
    s: 1rem
  ),
  grid-gap: (
    m: 7px,
    l: 10%
  )
);

:root {
  @include sbpm.create-breakpoints($custom-properties, $breakpoints, $base-name: m);
}
```

You can then reference your custom properties like usual:

```scss
.foo {
  margin-top: var(--margin-top);
}
```