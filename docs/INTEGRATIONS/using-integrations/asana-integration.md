---
title: Asana
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
Asana Integration allows you to seamlessly connect your Botpress and Asana, a well-established project management platform. This integration equips your chatbot with the ability to manage projects and tasks right from its interface. After the setup, you will be able to perform actions such as task creation, task updates, task comment addition, and more.

## Prerequisites

* An [Asana account](https://asana.com/)
* Access to an existing Asana workspace.

## Setting up the Asana integration in Botpress

1. Go to the [Integration Hub](https://app.botpress.cloud/hub) in Botpress Cloud (if you don't have the integration installed yet).
2. Find and open the Asana integration then click on the "Install to Bot" button, now go back to your bot settings.

The Asana integration has the following settings:

* **Enabled**: Whether Botpress will communicate with Asana
* **Webhook URL**: The URL for receiving data in Botpress. (You shall not be using it)
* **API Token**: The API token generated from Asana
* **Workspace Gid**: The workspace ID obtained from Asana

## Setting up Asana

1. Generate a Personal Access Token on Asana. Follow [these instructions](https://developers.asana.com/docs/personal-access-token) to get your token. Once you have it, paste it in the API Token input in Botpress.
2. Get the workspace ID. You can obtain your workspace ID by visiting [this link](https://app.asana.com/api/1.0/workspaces) while logged in to your Asana account. The workspace ID corresponds to the `gid` parameter of the workspace you want to use. Paste it in the Workspace Gid input in Botpress.

That's it! Now the Asana integration is operational and ready for use within your bot.

> 🚧 Note
>
> The Asana API rate limits are applicable. Also, note that certain advanced Asana features tied to paid plans may not be accessible.

<br />

## Capabilities

With the Asana Integration, you can interact with Asana directly from your Botpress chatbot. The integration introduces various actions, including task creation, task updates, task comment addition, and more, making the task and user management processes more efficient.

### Cards

Here's a breakdown of the Cards / functions provided by Asana Integration and their input fields. You need to make sure the integration is enabled before being able to add them.

#### Create task

This function is used to create a new task in Asana. The input fields include:

* **name**: The name of the task.
* **notes**: The description of the task (optional).
* **assignee**: The ID of the user who will be assigned to the task or "me" to assign to the current user (optional).
* **projects**: The project IDs should be strings separated by commas (optional).
* **parent**: The ID of the parent task (optional).
* **start\_on**: The start date of the task in `YYYY-MM-DD` format (optional).
* **due\_on**: The due date of the task without a specific time in `YYYY-MM-DD` format (optional).

You can store the output of this to a variable to access the permalink.

#### Update task

This function is used to update an existing task in Asana. The input fields include:

* **taskId**: The ID of the task to update.
* **name**: The name of the task (optional).
* **assignee**: The ID of the user who will be assigned to the task or "me" to assign to the current user (optional).
* **completed**: If the task is completed, enter "true" (without quotes), otherwise, it will keep its previous status (optional).

#### Find user

This function is used to find a user, and all their associated metadata in Asana. The input field is:

* **userId**: You should use the email of the user here.

#### Add comment to task

This function is used to add a comment to a task in Asana. The input fields include:

* **taskId**: The ID of the task to comment.
* **comment**: The content of the comment to be added.

***

With Asana Integration, your Botpress chatbot becomes a powerful project management tool that can interact with Asana directly. This facilitates efficient task and user management processes, saving you time and improving your productivity. Whether you're creating a task, updating an existing one, finding a user, or adding a comment to a task, Botpress Asana Integration makes it all possible right from your chatbot interface.
