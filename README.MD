## import

- `@import <link>`

## Varibles

- `$<variables_name>`

## Partial

- partial means this file won't be created but would be compiled by gulp
- a partial file is created by giving the file a name starting with `_`
- example `_variables.scss`

## ordering of import

- Keep the ordering proper because it matters.
- order should be like this
  - 1. variables & functions
  - 2. base & layout
  - 3. colors
  - 5. components (button, card, navbar)
  - 6. utilities (margin, padding, opacity)

## nested classes

- example: `.card{
  .card-title{

  }
  .card-body{

  }
  }`

## use of mathematical operator in varaible declaration as well as in the property

- we can directly use the mathematical operator with the variables
- example `$base-font-size:1rem;
   $font-size-sm: $base-font-size * 0.75;
   $font-size-lg: $base-font-size * 1.5;
`

- we need to use `math package` to apply mathematica operations inside the classes
- example `@use "sass:math";
.card{
  border-radius: math.div($base-border-radius, 4);
}
`

## we can debug in scss

- using `@debug`;
- example - `@debug "hello ninjas";`, `@debug math.div(10,3);`, `@debug math.max(1px,20px,15px);`

## maps

- we can create a map in the scss
- example - `
  $colors(
        "primary":$<variable>,
  "secondary":#11111
  );
- functions: map-has-key($colors,"primary"), map-get($colors,"primary"),map-remove($colors,"secondary"),map-merge($colors,("purple":#1920e,"green":#09121))

## loops

- @each $key, $val in $colors {
  .text-#{$key} {
  color: $val;
  }
  // light variations
  @for $i from 1 through 9 {
    .text-#{$key}-light-#{$i} {
  color: mix(white, $val, $i \* 10);
  }
  }
  }

## conditionals

- `@if (10>5) {
   .test-if {
    color: black;
  }
  }@else {
    .test-if-2 {
     color: white;
  }
}
`

# effect like hover:

- we can add multiple effects using nesting
- example: `.text-hover-#{$key} {
                &:hover {
                  color: $val;
              }
              &:last-child{
                color:mix(white,$val,10);
              }
            }
         `


## mixins and include
- To remove the redundance of the same property 
- @mixin btn($bg-color: #e2e2e2) {
  text-decoration: none;
  cursor: pointer;
  display: inline-block;
  border: 0;
  padding: $base-padding $base-padding * 2;
  border-radius: $base-border-radius;
  background-color: $bg-color;
}
.btn {
  @include btn();
}
@each $key, $val in $colors {
  .btn-#{$key} {
    @include btn($val);
    &:hover {
      background-color: lighten($val, 5);
    }
  }
  .btn-outlined-#{$key} {
    @include btn(#fff);
    border: $base-border-thickness solid $val;
    &:hover {
      background-color: $val;
    }
  }
}
