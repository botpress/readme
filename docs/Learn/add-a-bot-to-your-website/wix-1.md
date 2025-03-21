---
title: Wix
excerpt: Add a bot to your Wix website using Webchat.
deprecated: false
hidden: false
metadata:
  robots: index
---
> 🧩 Prerequisites
>
> * A [published bot](https://botpress-docs.readme.io/v1.5/docs/build#/)
> * A Wix website with a [plan that allows adding custom scripts](https://www.wix.com/plans)
> * A [domain connected to your Wix website](https://support.wix.com/en/article/connecting-a-domain-to-the-wix-name-servers)
> * Familiarity with HTML (if you want to [embed in an HTML div](#embed-in-an-html-div))

> 📺 Visual learner?
>
> Check out our [Wix guide](https://www.youtube.com/watch?v=rG7dguRDFIA\&t=1068s) on YouTube, which teaches you how to build and embed a bot on your Wix site.

You have several options for embedding a bot on your Wix website:

\<Tabs>
&#x20; \<Tab title="As a chat bubble">
&#x20;   \# Embed as a chat bubble

&#x20;   \## Step 1: Get your embed code

&#x20;   To embed a bot a bot on your Wix website, you need the bot's Webchat embed code. You can get the embed code from either the \[Studio]\() or your \[Webchat settings]\().

&#x20;   \### From the Studio

&#x20;   1\. Select \*\*Share\*\* in the upper-right corner.
&#x20;   2\. Select \*\*Configure\*\*, then copy the \`script\` tags:

&#x20;   \<Image align="center" src="https\://files.readme.io/fde8fb684e105e7dc3e04994924e40e5d2832cc3e1c5ca74efad7ce70fcbde4d-Screen\_Shot\_2025-03-20\_at\_10.16.22.png" />

&#x20;   \### From your Webchat settings

&#x20;   1\. Open your bot's Workspace. In the left navigation bar, find the bot you want to embed.
&#x20;   2\. Select \*\*Webchat\*\*, then open the \*\*Share\*\* tab.
&#x20;   3\. Copy the \*\*Embed code\*\*:

&#x20;   \## Step 2: Add to your Wix website

&#x20;   Next, add the Webchat embed code to your Wix website:

&#x20;   1\. Login to your \[Wix]\(https\://www\.wix.com) dashboard and select \*\*Settings\*\* in the left navigation bar.
&#x20;   2\. Scroll to \*\*Advanced Settings\*\*, then select \*\*Custom Code\*\*.
&#x20;   3\. Select \*\*+ Add Custom Code\*\*. Then, paste the Webchat embed code in code snippet field.
&#x20;   4\. Check the \*\*All pages\*\* option, then select \*\*Load code once\*\* from the drop-down menu.
&#x20;   5\. Check the \*\*Body - start\*\* option.
&#x20;   6\. Select \*\*Apply\*\*.
&#x20; \</Tab>

&#x20; \<Tab title="In an HTML div">
&#x20;   \# Embed in an HTML div

&#x20;   You can also embed your bot in an HTML div. This is useful if you want more control over where your bot appears on your Wix site.

&#x20;   \## Step 1: Get your Botpress credentials

&#x20;   To embed a bot in an HTML div, you need your Botpress Client ID and Bot ID.