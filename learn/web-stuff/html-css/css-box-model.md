---
description: How everything in CSS is Box and properties of it.
---

# CSS - Box model

### box-sizing <a href="#block_and_inline_boxes" id="block_and_inline_boxes"></a>

how the total width and height of an element is calculated.

* _**content-box**_ - Doesn't take account of border and padding size
* _**border-box**_ - Takes account for any border and padding in the values you specify for an element's width and height.

> ### Boxes have an **inner display type** and an **outer display type**.

### Common "outer display type" - block & inline and their behaviour

#### Block:

* The box will break onto a new line.
* The [`width`](https://developer.mozilla.org/en-US/docs/Web/CSS/width) and [`height`](https://developer.mozilla.org/en-US/docs/Web/CSS/height) properties are respected.
* Padding, margin and border will cause other elements to be pushed away from the box.
* The box will extend in the inline direction to fill the space available in its container. In most cases, the box will become as wide as its container, filling up 100% of the space available.

#### Inline:

* The box will not break onto a new line.
* The [`width`](https://developer.mozilla.org/en-US/docs/Web/CSS/width) and [`height`](https://developer.mozilla.org/en-US/docs/Web/CSS/height) properties will not apply.
* Vertical padding, margins, and borders will apply but will not cause other inline boxes to move away from the box.
* Horizontal padding, margins, and borders will apply and will cause other inline boxes to move away from the box.

#### inline-block

A middle ground between `inline` and `block`. Use it if you do not want an item to break onto a new line, but do want it to respect `width` and `height`

* The `width` and `height` properties are respected.
* `padding`, `margin`, and `border` will cause other elements to be pushed away from the box `(unlike inline both vertical/horizontal are effected)`.

### [Block and inline boxes](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building\_blocks/The\_box\_model#block\_and\_inline\_boxes)

In CSS we broadly have two types of boxes — **block boxes** and **inline boxes**. The type refers to how the box behaves in terms of page flow and in relation to other boxes on the page. Boxes have an **inner display type** and an **outer display type**.

In general, you can set various values for the display type using the [`display`](https://developer.mozilla.org/en-US/docs/Web/CSS/display) property, which can have various values.

### Inner display type - Flex, Grid

You can change the inner display type for example by setting `display: flex;`. The element will still use the outer display type `block` but this changes the inner display type to `flex`. Any direct children of this box will become flex items and behave according to the [Flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS\_layout/Flexbox) specification.

### **Margin collapsing**

Depending on whether two elements whose margins touch have positive or negative margins, the results will be different:

* Two positive margins will combine to become one margin. Its size will be equal to the largest individual margin.
* Two negative margins will collapse and the smallest (furthest from zero) value will be used.
* If one margin is negative, its value will be _subtracted_ from the total.
