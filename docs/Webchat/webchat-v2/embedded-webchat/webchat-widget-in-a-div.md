---
title: Embedding the webchat widget in an HTML element
excerpt: This allows you to embed the webchat widget within any html element.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Sometimes you'd like your webchat to fill a container and not be at the bottom right of your site.. 

There are two steps to get this to work. 

<br />

1. Change the parent container.

The first is adding code between the script tags to inject logic to open the webchat when it's ready and hide the floating action button. You can do so by adding the following code:

```html html
<script src="https://cdn.botpress.cloud/webchat/v2.2/inject.js"></script>
<!-- ADD THIS CODE -->
<script>
    window.botpress.on("webchat:ready", (error) => {
      window.botpress.open();
    });
</script>
  
<style>
.bpFab {
  display:none;
}

.bpWebchat {
  width:100%!important;
  height:100%!important;
}  
</style>
<!-- IN BETWEEN THE TWO SCRIPT TAGS -->

<script src="https://files.bpcontent.cloud/2024/10/29/14/YOUR_SCRIPT_TAG.js"></script>
```

<br />

> 🚧 Pitfall prevention
>
> You must make sure the added code is found between the two script tags.

Broken down, this is the javascript to add:

```javascript javascript
window.botpress.on("webchat:ready", (error) => {
      window.botpress.open();
    });
```

and this is the styles to add:

```Text CSS
.bpFab {
  display:none;
}

.bpWebchat {
  width:100%!important;
  height:100%!important;
}  
```

The styles affects the parent iframes to ensure that the chat bubble is always hidden, and the message container always shown.

<br />

2. Hide the close button in the messenger

Under Webchat -> Theme -> Styles add the following code:

```Text css
.bpHeaderContentActionsContainer :nth-child(2) {
    display: none;
}
```

Remember to press save at the bottom. This hides the close button, preventing the window from accidentally being closed.

That's it! You should be able to see your webchat taking the full height and width of your html container element!
