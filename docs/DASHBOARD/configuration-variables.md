---
title: Configuration Variables
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
![](https://files.readme.io/5ba8b2f-image.png)

Configuration Variables are containers that store essential information such as API keys and database credentials, and allow chatbot developers to easily access and modify them as needed. They provide a central location for configuration settings, which helps developers ensure that the chatbot functions correctly and stays up-to-date. Configuration variables also provide a level of security by keeping sensitive information separate from the codebase, reducing the risk of data exposure.

> 📘 **Note**
>
> Configuration Values set in Botpress Studio are for Development environment and Values set in Cloud Dashboard are for Production environment.

<br />

## Steps for using Configuration Variables

### 1. Env keys in Development

1. On the Left Panel in your Botpress Studio, Click the Botpress Icon and select **Chatbot Settings** -> **Variables**. You will see an option to add Configuration Variables.
2. Create a new Key and add the value that you want to use in your **Development** environment. Note that this value will should only be used while testing.
3. Click **save** and **publish** your chatbot.

### 2. Usage

You can use **`{{env.key}}`** to get the value of the Configuration Variable Key that you've created in step 1.

To use it in an Execute Code Card, you can write **`env.key`** to access it's value.

### 3. Env keys in Production

Go to Admin Dashboard, Select your chatbot and go to **Configuration Variables** tab. You can now set your key's production value here.

By following these steps, you can ensure that your chatbot has access to the necessary configuration variables in both your development and production environments. This can help to ensure that your chatbot functions properly and is able to provide
