# Sass Frontend Lesson

## This is the line of text being changed using different methods:
<p id="testing">original text and</p>

Welcome to our guide for Sass!

<!-- ![]({{site.baseurl}}/images/sassLogo.png) -->

## Examples:

We incorporated our SASS lesson concepts into two examples: A stopwatch and a calculator.

```scss
// example of @mixin
@mixin button {
  width: auto;
  height: auto;
  border-radius: 10px;
  background-color: #21807c;
  border: 3px solid black;
  font-size: 1.5em;

  display: flex;
  justify-content: center;
  align-items: center;

  grid-column: span 1;
  grid-row: span 1;

  // creates smooth animation effect
  transition: all 0.5s; 
}

// default button theme for calculator and stopwatch buttons. Both will follow the same button format
.button {
    // uses the scss from the @mixin
  @include button;
}

/* styling for the calculator clear button */
.calculator-button-clear {
    // @extend inherits .button and then changes the background color from .button
  @extend .button;
  background-color: #e68b1c;
}

/* styling for the calculator equals button */
.calculator-button-equals {
    // another @extend inherits .button and then changes the background color from .button
  @extend .button;
  background-color: #e70f0f;
}
```

Notes for expectations:
three UI's that are good:
- Github Pages or Sassy
- Bootstrap on a flask
- Tailwind
    - Focus on one UI
- If using Bootstrp or Tailwind, use flask

Assign HW: give 30 min of homework to play around with the code

- Do frontend on a game-centric plan or something like that and make changes on it using Sass
    - We can fix the snake game

Examples:
- We can make multiple examples(calculator, snake, etc.)
    - Then, we make same classes for all these different examples and use Sass so that the styling changes things of multiple examples.