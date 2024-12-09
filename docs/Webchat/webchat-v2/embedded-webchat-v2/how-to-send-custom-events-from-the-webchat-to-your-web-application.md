---
title: How to send custom events from the Webchat to your web application
deprecated: false
hidden: false
metadata:
  robots: index
---
You can setup your Bot to send custom events for your web application. To set this up:

1. In the Botpress Studio, add a "Send Custom Event" Card to a node.

   <Image align="center" width="75% " src="https://files.readme.io/8bf97791659b31730f63383d81ab348a388f7edb3b78fac34043d2f4e6263395-image.png" />
2. In your web application you can catch these like the following:

```javascript
window.botpress.on('customEvent', (event) => {
  console.log(event);
	// Your custom logic
});
```