---
title: Getting Started
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
# What are Botpress Integrations?

<Embed url="https://www.youtube.com/embed/67Bzbqh4B0w" href="https://www.youtube.com/embed/67Bzbqh4B0w" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252F67Bzbqh4B0w%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253D67Bzbqh4B0w%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252F67Bzbqh4B0w%252Fhqdefault.jpg%26key%3D7788cb384c9f4d5dbbdbeffd9fe4b92f%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22640%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

Integrations in Botpress are an easy and powerful way to extend Botpress channels, or improve the bot building experience.

Integrations have three main capabilities:

1. Connecting bots with messaging channels (e.g. Telegram, Facebook Messenger)
2. Extending Botpress Studio to add action cards that run any NodeJS code. (e.g. send an email, create a Jira ticket)
3. Extending Botpress Studio by adding event listeners, invokable by adding triggers. (e.g. get notified when a purchase is made)

They can be shared privately, or published to the Botpress Hub, where they can be discovered and installed by every Botpress user. They also run free of charge on Botpress Infrastructure, so you don't have to worry about hosting, scaling or even cost issues!

# Setting up your first integration

You can simply follow the instructions below.

## Prerequisites

* a workspace with a bot in Botpress Cloud
* your workspace handle must be set. You can do so by going to your [your workspace](https://app.botpress.cloud/workspaces/), clicking "Settings", and setting your workspace handle.

## Installing the integration to your workspace

Create a new integration project using the init command. This will create a new folder with the name you specified and generate a basic project structure.

1. Change `my-integration` with the name of your integration (no spaces), and run the following command.

```shell
INTEGRATION_NAME=my-integration
npx @botpress/cli init --name $INTEGRATION_NAME --type integration
cd $INTEGRATION_NAME
npm i --save-dev @growth-botpress/bp-integration-runner
npm i
```

bp-integration-runner allows you to easily run the integration locally, with hot-reloading and the ability to view logs locally.

2. Now add this script to your package.json file:

```json
{
  ...,
  "scripts": {
    "dev-local": "bp-integration-runner"
  },
  ...
}
```

Make sure to replace your package.json has an integrationName parameter such as `my-integration` with your integration name. The name is used as an id in combination with your workspace. It is not the display title for the integration, which is found in integration.definition.ts

3. Create a .env file which will contain your Botpress Personal Access Token and a Workspace ID to run your integration in dev mode. You can create an access token by visiting your [Botpress Cloud Profile Page](https://app.botpress.cloud/profile/settings) and clicking "Generate new token".

```Text .env
BOTPRESS_PAT=YOUR_PERSONAL_ACCESS_TOKEN
BOTPRESS_WORKSPACE_ID=YOUR_WORKSPACE_ID
```

We're now done with setup. We suggest you commit your repo at this point.

4. Create a .gitignore file in the root folder with the following content:

```bash .gitignore
.botpress
node_modules/
```

Now you can start developing your integration.

5. You can run the following command to start developing your integration:

```shell
npm run dev-local
```

6. When your integration is fully developed and tested, you can use the `npx bp login`, then `npx bp deploy` and finally reset the *Self hosted integration's url* in the settings section of your integration. This will allow the integration to run on Botpress infrastructure. Once deployed you will be able to see logs in you workspace in Botpress Cloud, under the integration, then the **logs** tab.

   The bp login command also asks you to select a workspace to deploy the integration to. Go to your workspaces and fetch the workspace\_id you'd like to deploy to.

<Image align="center" width="80% " src="https://files.readme.io/3a5c04394ae5fb156fcbe21f099b79780cfb550412d8612c77121138b4175446-image.png" />

<br />

## Adding the integration to your bot

1. After which, open [your workspace](https://app.botpress.cloud/workspaces/) and click "Your Integrations".
2. Find your integration and click "Install". Select the bot from your list of bots.
3. Once the integration is installed "Configure Integration"
4. Click the "Enable integration" toggle on the top right, then hit "Save" to enable the integration.

In the bot's integration page, you will be able to add configuration variables at a later point.

# Seeing your integration logs

To see the logs of your integration,

1. Open [your workspace](https://app.botpress.cloud/workspaces/) and click "Your Integrations".
2. Find your integration and click "Logs" to see the logs of your integration.

# Adding Capabilities

Now that you have your integration running and installed on your bot, you can start adding capabilities to it.

* [Adding Messaging Channel Capabilities](../docs/adding-messaging-channel-capabilities)
* [Adding Actions & Triggers to Botpress Studio](doc:adding-actions-triggers-to-botpress-studio)