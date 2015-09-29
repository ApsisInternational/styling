# Apsis CSS Styleguide

### Stylus
We use [Stylus](http://learnboost.github.io/stylus/) as our main CSS preprocessor.

### KSS
We always write [KSS](http://warpspire.com/kss/) documentation for our components to integrate them easier into Kitsune.

### Naming conventions

We prefix all our component classes with a_ i.e `.a_Modal`

We use [SUIT CSS](https://github.com/suitcss/suit/blob/master/doc/README.md) naming conventions:

- u-utilityName
- ComponentName
- ComponentName—modifierName
- ComponentName-descendentName
- ComponentName.is-stateOfComponent

Example:
```html
<div class=“a_Modal”>
  <header class=“a_Modal-header”>
    <img class=“a_Modal-icon” src=“{{src}}” alt=“{{alt}}”>
  </header>
  <div class=“a_Modal-bodyText”>Hello</div>
</div>
```

## Helper Mixins

We have a number of helper mixins to make our lives easier.

### Remify
*by David Wals*

Remify lets us turn pixel values into rem values, making it easier for us to get a sense of how much the value represents.

With a base font-size of 16px, this example:
```css
.a_Box {
    height: remify(100px);
    width: remify(250px);
}
```

Will compile into:
```css
.a_Box {
    height: 6.25rem;
    width: 15.625rem;
}
```

### Shadow

Our shadow helper applies a shadow on the element you declare it on.

Example:
```css
.a_Box {
    shadow(1);
}
```

Compiles into:
```css
.a_Box {
    box-shadow: 0 3px 3px rgba(0,0,0,0.05),0 3px 3px rgba(0,0,0,0.05);
}
```

## Syntax
- Use soft tabs with four spaces—they’re the only way to guarantee code renders the same in any environment.
- When grouping selectors, keep individual selectors to a single line.
- Include one space before the opening brace of declaration blocks for legibility.
- Place closing braces of declaration blocks on a new line.
- Include one space after : for each declaration.
- Each declaration should appear on its own line for more accurate error reporting.
- End all declarations with a semi-colon. The last declaration’s is optional, but your code is more error prone without it.
- Comma-separated property values should include a space after each comma (e.g., box-shadow).
- Don’t include spaces after commas within rgb(), rgba(), hsl(), hsla(), or rect() values. This helps differentiate multiple color values (comma, no space) from multiple property values (comma with space).
- Never use hard coded color values (i.e `#FFF`). We have color variables and all the color values should be extracted from there.
- Don’t prefix property values or color parameters with a leading zero (e.g., .5 instead of 0.5 and -.5px instead of -0.5px).
- Quote attribute values in selectors, e.g., input[type=“text”]. They’re only optional in some cases, and it’s a good practice for consistency.
- Avoid specifying units for zero values, e.g., margin: 0; instead of margin: 0px;.

Bad CSS:
```css
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #ccc,inset 0 1px 0 #FFFFFF
}
```

Good CSS:
```css
.a_Selector,
.a_Selector-secondary,
.a_Selector[type=“text”] {
  padding: 15px;
  margin-bottom: 15px;
  background-color: rgba(0,0,0,.5);
  box-shadow: 0 1px 2px COLORS['black']['500'], inset 0 1px 0 COLORS['white']['main'];
}
```

## Declaration order
Related property declarations should be grouped together following the order:

1. Positioning
2. Box model
3. Typographic
4. Visual

Positioning comes first because it can remove an element from the normal flow of the document and override box model related styles. The box model comes next as it dictates a component’s dimensions and placement.

Everything else takes place inside the component or without impacting the previous two sections, and thus they come last.

```css
.a_DeclarationOrder {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: ZINDEX.component;

  /* Box-model */
  display: block;
  float: right;
  width: remify(100px);
  height: remify(100px);

  /* Typography */
  line-height: 1.5;
  color: COLOR['black']['main'];
  text-align: center;

  /* Visual */
  background-color: COLORS['green']['400'];
  border: 1px solid COLORS['green']['800'];
  border-radius: BORDER.radiusLarge;

  /* Misc */
  opacity: 1;
}
```
