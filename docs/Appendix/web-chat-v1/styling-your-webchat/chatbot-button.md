---
title: Chatbot Button
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
![](https://files.readme.io/4b92221-image.png)

You can Customize the Chatbot Button using below CSS

```typescript
.bpw-floating-button {
    /* Aligns the button to the right side of the container */
    float: right;
    /* Sets the fill color of the button icon */
    fill: rgb(255, 255, 255);
    /* Changes the cursor to a pointer when hovering over the button */
    cursor: pointer;
    /* Removes the outline around the button when clicked */
    outline: none;

    /* Centers the icon inside the button element */
    display: flex;
    align-items: center;
    justify-content: center;

    /* Sets the z-index to ensure the button is on top of other elements */
    z-index: 1;
    /* Sets the width and height of the button */
    width: 52px;
    height: 52px;
    /* Changes the cursor to a pointer when hovering over the button */
    cursor: pointer;
    /* Rounds the corners of the button */
    border-radius: 50%;
    /* Adds a shadow effect to the button */
    box-shadow: 0 2px 6px 0 rgba(0, 0, 0, 0.4);
    /* Clips any content that overflows the button */
    overflow: hidden;

    /* Removes padding and borders from the button */
    padding: 0;
    border: none;
    background-clip: padding-box;

    /* Adds a transition effect to the button when its size changes */
    transition: width 1s, height 1s;
}
```

<br />

This class styles the icon inside the floating button

```typescript
.bpw-floating-button i {
    /* Adds a transition effect to the icon when its opacity changes */
    transition: opacity 0.3s ease;
    /* Sets the opacity of the icon to fully visible */
    opacity: 1;
    /* Inherit the fill and stroke color from the parent button element */
    fill: inherit;
    stroke: inherit;
    /* Sets the width of the icon to 100% of the parent button element */
    width: 100%;
    /* Removes padding and sets line-height to 0 to center the icon */
    padding: 0;
    line-height: 0;
}
```

<br />

```typescript
.bpw-floating-button .bpw-floating-button-unread {
    /* Displays the notification badge */
    display: block;
    /* Positions the badge to the top right of the button */
    position: absolute;
    right: 2px;
    bottom: 54px;
    /* Sets the width and height of the badge */
    width: 20px;
    height: 20px;
    /* Rounds the corners of the badge to make it circular */
    border-radius: 50%;
    /* Centers the text inside the badge */
    line-height: 20px;

    /* Sets the color of the text inside the badge */
    color: #fff;
    /* Sets the background color of the badge */
    background-color: #ff5d5d;
    /* Adds a shadow effect to the badge */
    box-shadow: 0 0 4px 0 rgba(0, 0, 0, 0.4);
}
```
