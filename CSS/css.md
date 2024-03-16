# Responsive Web Design (RWD)

Here's a breakdown of the provided notes on Responsive Web Design (RWD):

- **The Viewport:**

  - The viewport is the user's visible area of a web page.
  - **Setting The Viewport:**
    - HTML5 introduced a method to control the viewport using the `<meta>` tag.
    - The recommended `<meta>` viewport element to include in all web pages: `<meta name="viewport" content="width=device-width, initial-scale=1.0">`.

- **Grid-View:**

  - Many web pages use a grid-view, dividing the page into columns.
  - Ensure all HTML elements have the `box-sizing` property set to `border-box`, ensuring padding and border are included in total width and height.
  - Add the following CSS code to set `box-sizing: border-box` for all elements: `* { box-sizing: border-box; }`.

- **Media Query:**

  - Media query is a CSS technique introduced in CSS3.
  - It uses the `@media` rule to include a block of CSS properties only if a certain condition is true.

- **Always Design for Mobile First:**
  - Designing for mobile before desktop or any other device is known as Mobile First.
  - This approach makes the page display faster on smaller devices, emphasizing responsive design.
  - CSS changes are required to implement Mobile First design effectively.

These notes provide an overview of essential concepts in Responsive Web Design, including viewport settings, grid-view, media queries, and the Mobile First approach.
