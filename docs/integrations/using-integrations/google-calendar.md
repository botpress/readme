---
title: Google Calendar
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
The Google Calendar Integration for Botpress enables your bot to access and create Google Calendar data in real-time, automating workflows like CRM updates, inventory management, and survey tracking directly within chat.

### Google Console

- First, you need to access: <https://console.developers.google.com/>
- [Log](<>) in with your Google account
- Next to the Google logo, click on the dropdown list
- After clicking on the dropdown list in the image, a modal will open and you should click on **New Project**  ![In this image, the name is listed as Botpress Google Sheet because it is an integration that was already set up previously.](https://files.readme.io/1febd82ea9049e86fedefeea48c65ca775b2bf8d4442d961a95b6664f21bbc94-Screenshot_2024-10-08_at_11.54.50_AM_1.png)  
    In this image, the name is listed as Botpress Google Sheet because it is an integration that was already set up previously.
- You will need to enter your project information such as:
  - Project name
  - Organization
  - Location  
    ![In this case, the name of my project is Tutorial Botpress Integration, but feel free to choose your own name.](https://files.readme.io/228a79f40eea49c5a627ee2f973440d7ed9768b03b5e1f0fa50d83f3b08ad1af-Screenshot_2024-10-08_at_12.02.13_PM_1.png)  
    In this case, the name of my project is Tutorial Botpress Integration, but feel free to choose your own name.
- Then click on the create button
- To make sure you are in the correct project, check the project name next to the Google logo  ![Screenshot 2024-10-08 at 1.04.26 PM.png](https://files.readme.io/e88ee7b4ef6235bb1ac9dc5b4f1a5d51b88937cad256aa2090b17a404e2b0d03-Screenshot_2024-10-08_at_1.04.26_PM_1.png)
- The next step is to click on Menu → API & Services → Credentials  
    ![Screenshot 2024-10-08 at 1.05.45 PM.png](https://files.readme.io/d7be141d48c0ac12dc7536bd424ba787737560cb5fbf0ba40fa72e5d0bdb3cff-Screenshot_2024-10-08_at_1.05.45_PM_1.png)
- Click on Create Credentials → API Key to create an API key  ![Screenshot 2024-10-08 at 1.08.55 PM.png](https://files.readme.io/ca2ac62991c57175c7830d68568a8491f55a3bee5f6f008beb39f1eca840ecd3-Screenshot_2024-10-08_at_1.08.55_PM_1.png)
- The next step is to click on library and in the screen that opens, search for Calendar and enable the Google Calendar API  
    ![Screenshot 2024-10-08 at 1.28.57 PM.png](https://files.readme.io/4b7df7d1e66e57122801d51568a361bd70fe49c51f2b34b86e2953950b576e6a-Screenshot_2024-10-08_at_1.28.57_PM_1.png)  ![Screenshot 2024-11-18 at 1.35.03 PM.png](https://files.readme.io/1755347f29c350b4becc474bc5252fc2e2fe3b15c1f9a716e97ee6384b12e080-Screenshot_2024-11-18_at_1.35.03_PM.png)
- The next step is to create a Service Account
- Still in the Menu → API & Services → Credentials  ![Screenshot 2024-10-08 at 1.51.23 PM.png](https://files.readme.io/f9c0945941523f79372c14e2b82aeb95342cd6d19fc4cf0bb10ee14b51e5461d-Screenshot_2024-10-08_at_1.51.23_PM_1.png)
- Fill in the information. When the service account name is filled, the Service Account ID will be automatically generated  
  ![image.png](https://files.readme.io/c4ca91dd05fbc4621e6c19d2f463d028ee61024b2c00b9079dedba84e3d6f449-image_9.png)
- The other fields are optional and do not need to be filled in, so after defining the Service Account Name, just click on **Done**
- After the Service is created, you should go to the **KEYS** tab  ![image.png](https://files.readme.io/979f85b6f20e3ab349ff210cc9c064eec2bd6b5c1ea6e249b531e9e0e4270ec1-image_9.png)
- A modal will open where you will select JSON → Create  ![Screenshot 2024-11-18 at 1.49.33 PM.png](https://files.readme.io/4a55439eea21fda7cf08d972fd8e08dd7235d9617c410ce0461a2af2f98956b8-Screenshot_2024-11-18_at_1.49.33_PM.png)
- A JSON file will be downloaded to your machine and we will use this information in our integration with the Botpress bot
- Your JSON should look like this (in this case, I've omitted the values as they are sensitive information):
  ```jsx
  {
    "type": "",
    "project_id": "",
    "private_key_id": "",
    "private_key": "",
    "client_email": "",
    "client_id": "",
    "auth_uri": "",
    "token_uri": "",
    "auth_provider_x509_cert_url": "",
    "client_x509_cert_url": "",
    "universe_domain": ""
  }
  ```

### Creating OAuth client ID

- After generating the JSON file, you'll need to create the **OAuth Client ID** authentication  ![image.png](https://files.readme.io/4904a59386335fd0a60cd000716e17b5b9a9871feb1eae946829e2407bba6716-image_9.png)
- You'll need to select an Application Type and also create a name, then click on **CREATE**  
  ![image.png](https://files.readme.io/1ccfa044ba86eb45f7a90e2938ebda88dbb0d96d8d9c5f5c59baaf92c5d0fbfc-image_9.png)

### Creating OAuth Consent Screen

- After creating the OAuth, you'll need to create the OAuth consent screen
- Create an App name and for User support email, just select your email  
  ![image.png](https://files.readme.io/2a7ded6b93543d3ec651580e74da51be4dcf132b41d3263be0a133957633610b-image_9.png)
- Further down, you'll need to create the App domain, where you'll need to enter the URL of your calendar for both the Application home page and Application privacy policy link. But if you have another URL for this information, you can use it  
  ![image.png](https://files.readme.io/73ae329f57d19bf35d44d801837628e586b5cc827437662811811e87f5d946c9-image_9.png)
- In **Authorized domain**, you'll need to add at least [google.com](http://google.com) as shown in the image below
- Also add a contact email, in this case, the developer's email can be any email
- After entering this information, click on **SAVE AND CONTINUE**  ![image.png](https://files.readme.io/36f58eb3af56e024d702a9eae02ed891e11a203a2b644a98893d3eb46592e06a-image_9.png)

### Scopes

- You should add some scopes by clicking on the button as shown in the image below  ![image.png](https://files.readme.io/a60dc6a983d6b7fa055e19b3196856ede365d1f8e3b7d4ffb68a78a199d983f2-image_9.png)
- Below I will provide the list of all scopes that should be added for the integration to work correctly  
    ![Screenshot 2024-11-18 at 3.35.12 PM.png](https://files.readme.io/3774fac9362258f051674498166517483e610a2ac67c235d3e13702fa181902a-Screenshot_2024-11-18_at_3.35.12_PM.png)  
    ![Screenshot 2024-11-18 at 3.35.55 PM.png](https://files.readme.io/c375a649cec9614bd53d31009cbfef0a2b30aea0183146eff5fdbd993cb1c508-Screenshot_2024-11-18_at_3.35.55_PM.png)
- Then you'll need to provide some justifications for why you're using the scopes. Just explain that the bot needs the scopes to create, delete, update, and read
- You'll also need to provide a YouTube demo link. You can use whichever one you find necessary  ![image.png](https://files.readme.io/3cadcb96adef95071c9a7aab8bf1d90bd249dd276ffa4258a0a7b9cf87487622-image_9.png)

### Google Calendar Authorizations

- In your Google Calendar dashboard
- You'll need to go to your calendar settings
- To do this, just click on the gear icon in the upper corner as shown in the image below  ![image.png](https://files.readme.io/4b7e7dc50cab92596d4dd6adc33fb7ba9a13d1a90d56ba18182c7b8d0e33fdb7-image_9.png)
- The next step is to click on your calendar  
    ![image.png](https://files.readme.io/31c076eaac192672f016d7cf54452d006b9fe3fe62e34f3e3f414abf4c606341-image_9.png)
- After selecting the calendar, you should add the email that the bot uses in its integration  
  ![image.png](https://files.readme.io/29a3b7556fe9fe96faa8a9fbc5902d9639af388bc3356337c16234e371ccfcd3-image_9.png)
- To know the email that the bot uses, you should consult the JSON file you downloaded
  - Open the downloaded JSON file, you can use any text editor for this
  - Copy the client_email
  - Paste the email to be added
- After adding the email, you should change its permission so that it can make changes to events

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7ff97c7def06e5f76914de8c00c1026f10ed90b274104233efe09d8618b9ddf7-Screenshot_2024-11-18_at_4.33.35_PM.png",
        null,
        "Screenshot 2024-11-18 at 4.33.35 PM.png"
      ],
      "align": "center"
    }
  ]
}
[/block]


### Bot Integration Settings

- In your Botpress Studio, in the upper corner, you should install the integration  
  ![image.png](https://files.readme.io/40958c6e77385f7f63011ef7b710e13a4dd2de83aea5f134e448518532149306-image_9.png)
- Search for the Google Calendar integration verified by Botpress and install it  
    ![image.png](https://files.readme.io/b75eb013c354e6d6c26f6567a310b13cdf0f5c1cb2e26610355ffd76099c72b8-image_9.png)
- After installation, you should change the configuration to configure manually  ![image.png](https://files.readme.io/fae2ca4224a214592df211e6687637150d50b82deb37852188a6f898abc9b6b9-image_9.png)
- You'll need to enter the necessary information to perform the integration  
  ![image.png](https://files.readme.io/a61633af29b62017edcf3268f6c757ab644c640477e1befec47f1aa1d6671c71-image_9.png)
- To get the Calendar ID information, you should go to settings as you did before
- Select your calendar → Integrate calendar, you will find your Calendar ID as shown in the image below  ![image.png](https://files.readme.io/2c89f1638f88ad33cc2ecf59a02f8beeb591765d06708783ee4801dc659155d1-image_9.png)
- For the other integration information, you can find everything in the JSON file you downloaded and should use the **client_email** and **private_key**
- After that, click on **Save Configuration**
- After these steps, you can use Google Calendar in your bot.