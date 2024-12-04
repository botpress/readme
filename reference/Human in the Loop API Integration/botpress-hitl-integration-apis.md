---
title: How to use the Botpress Human in the Loop API Integration
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
> 📘 Read this first!
>
> * If you are looking to use the built-in agent-handoff feature, read the [HITL](doc:hitl-1) guides.
> * Otherwise, if you are comfortable with Javascript or typescript, you should use Botpress's HITL Interface: [Connect a live agent platform with Botpress](doc:revised-hitl). 
> * This is for developers who want to use an external platform, and who do not wish to use javascript or typescript to build a connector.

The  ([Human in the Loop API integration](https://app.botpress.cloud/hub/integrations/intver_01J804C5W78Y5FWHHNVWMR5VM3)) serves two purposes.

1. It allows you to write a live agent connector to your platform using any language / tech stack.
2. It serves as a great example for understanding how to build a Botpress integration that does this.

## Usage

1. Install the integration on a Botpress bot in the studio.
2. Set up an endpoint service and make it publicly available. 
3. Add the endpoint base url to the integration configuration in the Botpress Studio and hit save. You should get an error, this is likely because you haven't implemented a "/ping" route yet.
4. Go through each of [Endpoints to implement](ref:endpoints-to-implement) and implement a route on your server that returns the correct response and takes the payload. The endpoints handle requests from Botpress to your live agent platform. All five endpoints must return a http 200 header. Aside from that, two endpoints ( creating a conversation, and creating a user) require you to return the id of the resource that was created. This allows Botpress to route the messages to / from the right users & tickets. 
5. In your service, you should call the endpoints listed in [Calling the API](ref:calling-the-api) to interact with with user. These handle requests from your live agent platform to Botpress.
6. Once that's done, hit "save" again to make sure the ping route is accessed.
7. Make sure the "HITL Agent" is on, and the HITL-API agent is selected.
8. In your conversation flow, add the "Escalate to a human" card, and configure its fields.
9. Publish your bot, then try sending messages back and forth.

<br />

<br />

<Image alt="This is the integration that allows communication via API for non js/ts devs" align="center" src="https://files.readme.io/5130dae22c15bc1503db06b18023c6257e86c3ce345def3d103ef3cace3d5916-image.png">
  This is the integration that allows communication via API for non js/ts devs
</Image>

<Image alt="This is the no-code integration that allows Botpress users to act as live agents" align="center" src="https://files.readme.io/6894784c708ced81502a31fa0e368c36a2a640ee43d0b2a8e5aefd4ecf2afb29-image.png">
  This is the no-code integration that allows Botpress users to act as live agents
</Image>
