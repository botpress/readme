---
title: Listening to webchat events
deprecated: false
hidden: true
metadata:
  robots: index
---
You can listen to a number of webchat events and plug in your handler logic for more customized workflows.

### Listen to webchat ready

This event is fired when the webchat client is initialized and ready.

```javascript
window.botpress.on('webchat:ready', (conversationId) => {
	console.log('webchat is ready: ', conversationId);
  // INSERT YOUR LOGIC HERE
});
```

### Listen to webchat opened / closed

These event is fired when the webchat component is opened or closed.

```javascript
window.botpress.on('webchat:opened', (conversationId) => {
	console.log('webchat was opened ', conversationId);
  // INSERT YOUR LOGIC HERE
});

window.botpress.on('webchat:closed', (conversationId) => {
	console.log('webchat was closed ', conversationId);
  // INSERT YOUR LOGIC HERE
});
```

### Listen to conversation

This event is fired when a new conversation is started

```javascript
window.botpress.on('conversation', (conversationId) => {
	console.log('conversation id: ', conversationId);
  // INSERT YOUR LOGIC HERE
});
```

### Listen to message

This event is fired when a message is sent by the bot.

```javascript
window.botpress.on('message', (message) => {
	console.log('message received: ', message);
  // INSERT YOUR LOGIC HERE
});
```

### Listen to messageSent

This event is fired when a message is sent by the user.

```
window.botpress.on('messageSent', (message) => {
	console.log('sent message: ', message);
  // INSERT YOUR LOGIC HERE
});
```

### Listen to error

This event is fired when there is a error in the bot

```
window.botpress.on('error', (error) => {
	console.log('error: ', error);
  // INSERT YOUR LOGIC HERE
});
```

### Listen to custom event

This event is fired when a custom event is triggered from the bot

```javascript
window.botpress.on('customEvent', (event) => {
  console.log(event);
	// INSERT YOUR LOGIC HERE
});
```