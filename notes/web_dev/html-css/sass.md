### Sass

```scss
h1, h2, h3 {
  //Equivalent to h1.lg-heading
  &.lg-heading{}
 	//Affects any nested elements w/in h1/h2/h3 with the specified class name
  .lg-heading{}
}
```

- 6rem is 6 times the rem unit
  - rem unit is a multiplier of the html tag's font size (default is 16 pixels)

- z-index is how close an element is to you (layering)

```scss
//Allows the same transition to be used uniformly throughout a file
@mixin easeOut(){
	transition: all 0.5s ease-out;
}

a {
  //& uses the element it is nested in 
  &:hover {
    color: $secondary-color
    @include easeOut();
  }
}

```



- vh & vw slice the screen into numerous slices of height and width
  - 100 vh and 100 vw takes up whole screen
  - 10 vh takes 10 slices of the height
- rgba(color,opacity) Sets the color and opacity for a property 
  - stands for red green blue alpha 
