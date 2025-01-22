---
title: Improvement
excerpt: Provide feedback on specific LLMz iterations to improve future conversations.
deprecated: false
hidden: false
metadata:
  robots: index
---
> 🚧 Early Beta
>
> The Improvement integration is in beta and should not be used in production or critical workflows. We encourage testing in non-production environments and welcome your feedback to improve its stability and functionality.
>
> Each stored iteration uses your Workspace's Table Rows quota, and may demonstrate increased usage.

# How to use

## Install

Start by installing the Improvement integration from the integration hub.

[Link to integration](https://studio.botpress.cloud?exploreHub=1\&hubItemId=intver_01JDTX5RMZGB170E630HS62GAR)

<Image align="center" className="border" border={true} src="https://files.readme.io/34580f93384f4cf1c30342e133594909942497bb5d01fb5cdb663882e4038439-Screenshot_2025-01-22_at_2.45.42_PM.png" />

## Store Iterations

After installing the integration, all of the iterations produced by LLMz via an Autonomous Node will be stored in the automatically-created "LLMz iterations" Table. Iterations are produced at the message level, meaning a single conversation will typically have multiple iterations.

<Image align="center" className="border" border={true} src="https://files.readme.io/770d7ff0ceb1fbe2606247dbddf3e0f5d014e0ec2d83fa5a1e79329866bf6acc-Screenshot_2025-01-22_at_2.48.58_PM.png" />

This table is automatically populated every time an iteration ends. Each iteration takes up its own record, and stores specific data like the conversation or event ID, along with the iteration itself.

## Provide Feedback

Once you've installed the Improvement integration, you can access the "Improvement" window through the "Views" button on the top-right corner of the Studio.

<Image align="center" className="border" border={true} src="https://files.readme.io/bbd9fa247fe15a216c2017bf6a978e052da6f4bb61e519ab6af980577eb4aa36-Screenshot_2025-01-22_at_2.54.24_PM.png" />

You can access the Improvements UI from this menu.

<Image align="center" src="https://files.readme.io/0b7cbcd48bed41418333c7b39252eab15ee772b41e32fe407cdf99a7cd95b0e3-Screenshot_2025-01-22_at_2.55.25_PM.png" />

The Improvements UI shows all of your bot's conversations, along with each individual LLMz iteration. This iteration is the code your bot generated to take an action and/or respond to the user.

Hovering over a specific iteration will let you access the Feedback window, in which you can suggest improvements to future iterations of similar tasks.

<Image align="center" src="https://files.readme.io/d26773428dd5db744eedbd80793b5107e37b8fef88a43495483fc87aa19d1923-Screenshot_2025-01-22_at_2.56.57_PM.png" />

Clicking "Re-generate" will produce a new iteration for your review. Once you're satisfied with the new iteration, clicking "Save" will store this to your bot's "Feedback" Table.

Your bot uses the information stored in its "Feedback" Table to inform future LLMz iterations.

<Image align="center" className="border" border={true} src="https://files.readme.io/dab272936c19dc0bc907a525ae0cbe8add937747b8ad08e0a9e76dd100ff5cc5-Screenshot_2025-01-22_at_3.00.39_PM.png" />