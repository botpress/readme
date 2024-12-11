---
title: Publish your integration on Botpress Hub
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
We're thrilled you want to publish your integration on the Botpress Hub! There is not much to do to make your integration publicly available to the other Botpress users, you're only a few steps away:

1. navigate to your integration's page on the dashboard
2. Whenever you integration is private, you'll see a blue banner with a **Make Public** button, just click on it.
3. Accept the hub terms and conditions and you're good to go.

<Image align="center" src="https://files.readme.io/f3ec409-Screenshot_2024-08-08_at_3.21.15_PM.png" />

# Getting your integration Verified :white_check_mark:

To ensure the quality of contributions on the Botpress Hub, we've come up with the following verification process. You can follow the instructions below or follow along the video. There are four things to do, follow along in the video:  

1. Update your profile on Botpress Cloud.
2. Update your integration's display information.
3. Ensure your integration checks the configuration parameters if any.
4. Prepare an example bot with your integration configured an
5. Send it for approval

<Embed url="https://www.youtube.com/embed/QJbqatyXfwI" title="How to publish to Botpress Hub" favicon="https://www.youtube.com/favicon.ico" image="https://i.ytimg.com/vi/QJbqatyXfwI/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/embed/QJbqatyXfwI" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FQJbqatyXfwI%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DQJbqatyXfwI%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FQJbqatyXfwI%252Fhqdefault.jpg%26key%3D02466f963b9b4bb8845a05b53d3235d7%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22640%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

<br />

## Your profile on Botpress Hub

When a user installs your app, your workspace information will be viewable by the user. Please ensure:

* [ ]  Your Workspace has a url handle that represents you.
* [ ]  You have a way for users to contact you, like an email or a website.
* [ ]  Introduce yourself in the Workspace description (optional). This is the place for self-promotion.
* [ ]  Add an icon to your Workspace that represents you (optional). 

We suggest you create a Workspace specifically for publishing integrations, as this will make it easier to add collaborators to your workspace, and keep your production and dev environments separate.

## Your integration's display information

Now we need to ensure the integration has all the assets and information it needs to be displayed on the Hub. 

Your integration's integration.definition.ts file should contain:

* [ ]  **title**: the display title of your integration for the hub. Do not include “Botpress”.
* [ ]  **name**: your\_workspace\_handle/integration\_handle
* [ ]  **description**: a succinct description of what your integration does.
* [ ]  **icon**: set this to 'icon.svg'.
* [ ]  **readme**: set this to 'hub.md'.

Make sure to have these two files in the root of your integration folder:

* [ ] icon.svg :  Use a pertinent icon related to the problem you are solving. Do not use the Botpress Icon.
* [ ] hub.md :  It should contain an explanation of what the integration is, and how to use it. Self-promotion is not allowed here. Please also add a link to git repo if your integration is open source, this drastically increase your chances of getting approved.

## Your integration's logic

Finally, we need to ensure your integration is robust and user-friendly.

* [ ]  If your integration requires parameters to be configured: it should validate the parameters in the register method, and throw a RuntimeError if there is an issue.

```
import * as bpclient from "@botpress/client";

...

throw new RuntimeError(
	"Configuration Error! The Mixpanel token is not set. Please set it in your bot integration configuration."
);
```

This RuntimeError will be shown to the user in the Botpress Studio when they try to add your integration to their bot and there is an issue.

## Submitting your integration for verification

When you're done with above, we'd like to test your integration to ensure it works as expected, and that everything is in order. Whenever you're ready , just click the "Request Verification" button on the banner.

<Image align="center" src="https://files.readme.io/3b20967-Screenshot_2024-08-08_at_3.30.44_PM.png" />

To speed up the process, you can do the following proactively

* [ ]  In your workspace, create a demonstration bot and configure your integration for it. We'll use this to try out the integration.
* [ ]  Add `hub-applications@botpress.com` to your workspace with Admin privileges.

If you have any questions whatsoever, please don't hesitate to reach out to us at [hub-applications@botpress.com](mailto:hub-applications@botpress.com)!
