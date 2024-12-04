---
title: Google Sheet
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
The Google Sheets Integration for Botpress enables your bot to access and update Google Sheets data in real-time, automating workflows like CRM updates, inventory management, and survey tracking directly within chat.

# Setting up Google Cloud

**Register Cloud Project**

* First, you need to access: [https://console.developers.google.com/](https://console.developers.google.com/)
* Log in with your Google account
* Next to the Google logo, click on the dropdown list\
    ![In this image, the name is listed as Botpress Google Sheet because it is an integration that was already set up previously.](https://files.readme.io/91def49a37f9253a10b7f1ee53c4f6fa5b6bede8f8407a998fbcd7b2be4c4e88-Screenshot_2024-10-08_at_11.54.50_AM.png)\
    In this image, the name is listed as Botpress Google Sheet because it is an integration that was already set up previously.
* After clicking on the dropdown list in the image, a modal will open, and you should click on **New Project**\
    ![Screenshot 2024-10-08 at 11.58.18 AM.png](https://files.readme.io/de0b5f45ad0ee8cdf424bda71915b25cde85c930a08b7d7c5a6a831d2b5c0b87-Screenshot_2024-10-08_at_11.58.18_AM.png)
* You will need to enter your project information such as:
  * Project name
  * Organization
  * Location\
    ![In this case, the name of my project is Tutorial Botpress Integration, but feel free to choose your own name.](https://files.readme.io/668a3177c3e25c8dd179038c2bd1902cecf4bb0b478bd7a33c6ebd288dd8e7e6-Screenshot_2024-10-08_at_12.02.13_PM.png)\
    In this case, the name of my project is Tutorial Botpress Integration, but feel free to choose your own name.
* Then click on the create button
* To make sure you are in the correct project, check the project name next to the Google logo\
    ![Screenshot 2024-10-08 at 1.04.26 PM.png](https://files.readme.io/29b1d578703dc609c8111406b5cf257ec18e59c789b9007b71a1e166e42b47e8-Screenshot_2024-10-08_at_1.04.26_PM.png)

**Create Project Credentials**

* The next step is to click on Menu → API & Services → Credentials\
    ![Screenshot 2024-10-08 at 1.05.45 PM.png](https://files.readme.io/12d74ee7f4d1e2bb05515531ae8bf53ded80bdfed010ae1a12da7d66a39c80a1-Screenshot_2024-10-08_at_1.05.45_PM.png)
* Click on Create Credentials → API Key to create an API key\
  ![Screenshot 2024-10-08 at 1.08.55 PM.png](https://files.readme.io/862c3963175a43a113f778d64f5f2aee49bef2a0372288142de06477046bd3a5-Screenshot_2024-10-08_at_1.08.55_PM.png)

**Enable Google Sheet API**

* The next step is to click on library and in the screen that opens, search for Sheet and enable the Google Sheet API\
    ![Screenshot 2024-10-08 at 1.28.57 PM.png](https://files.readme.io/082bdb874eb1dfd8462f6898aa35728264fc31726ca46c369d64f87f4e07ffd0-Screenshot_2024-10-08_at_1.28.57_PM.png)\
    ![Screenshot 2024-10-08 at 1.30.54 PM.png](https://files.readme.io/b2dde77e3d04b909eed93a5750ee71e33092a63c0661b115df7ee67bd60114af-Screenshot_2024-10-08_at_1.30.54_PM.png)

**Register Service Account**

* The next step is to create a Service Account
* Still in the Menu → API & Services → Credentials  ![Screenshot 2024-10-08 at 1.51.23 PM.png](https://files.readme.io/00c31180886818b7ddc51055240285e93a7de4a3f0c0caddbc354e997d635d3f-Screenshot_2024-10-08_at_1.51.23_PM.png)
* Fill in the information. When the service account name is filled, the Service Account ID will be automatically generated  ![Screenshot 2024-10-08 at 1.56.19 PM.png](https://files.readme.io/5a01f47f225d1ba1a17f1d46e855b02f64abe6f0418601372a96f5ad418eb74a-Screenshot_2024-10-08_at_1.56.19_PM.png)
* The other fields are optional and do not need to be filled in, so after defining the Service Account Name, just click on **Done**

**Create and Download Json Key**

* After the Service is created, you should go to the KEYS tab  ![Screenshot 2024-10-08 at 1.59.17 PM.png](https://files.readme.io/fb31c9d74eb3fe86ae13a78c209bbeea5eb629d0db959fb8ac179e16c6aa2d46-Screenshot_2024-10-08_at_1.59.17_PM.png)
* You will need to create a Key, for this click on Add Key → Create new key  ![Screenshot 2024-10-08 at 2.00.15 PM.png](https://files.readme.io/9940f89bf64d9622e0ba11a56f81ddbac5a1c84a400aa018e25472ccbd6fb2ac-Screenshot_2024-10-08_at_2.00.15_PM.png)
* A modal will open where you will select JSON → Create\
    ![Screenshot 2024-10-08 at 2.02.50 PM.png](https://files.readme.io/1e5e34b7c668a73f1e9d063d75966276cc6ebed3ca489b2a03bd399c9477e780-Screenshot_2024-10-08_at_2.02.50_PM.png)
* A JSON file will be downloaded to your machine and we will use this information in our integration with the Botpress bot
* Your JSON should look like this, in this case I omitted the values because it's sensitive information:

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

* With the configurations in the Google Console done, now we need to share the Sheet that the bot will view. To do this, you should:
  * Open the JSON that was downloaded, you can use any text editor for this
  * Copy the client\_email
  * Use this email as a way of sharing, as this will be the email that the bot will need and will use to connect to your spreadsheet
  # Setting up Sheet
* To share your spreadsheet in Google Sheet:
  * In the upper right corner you will see this image and click on it\
      ![Screenshot 2024-10-08 at 2.15.00 PM.png](https://files.readme.io/9dc708956efc0252d9cfaaac33849c8dcb7af2b60700747ed7c69d2a3b5056ff-Screenshot_2024-10-08_at_2.15.00_PM.png)
  * You should change the access and set it to allow anyone with the link\
      ![Screenshot 2024-10-08 at 2.17.13 PM.png](https://files.readme.io/633279d070678894787ae877531541839bbbbf8c12ed0ee00743bfb8f2a1de02-Screenshot_2024-10-08_at_2.17.13_PM.png)
  * And add the email generated by your JSON as if you were inviting the bot to have access to your spreadsheet
  * Now it's time to configure the integration in Botpress Studio
  * In your Studio, activate the integration with Google Sheet
  # Setting up Botpress Studio
  * Complete the required information in your Botpress Studio:
    * SpreadSheetID: This will be the id of your Sheet and to find the ID you should go to your Sheet and copy only the ID that your spreadsheet uses as shown in the image below\
      ![It’s important to remember to copy only the ID and not the entire URL.](https://files.readme.io/a8b90b98ed69ce53ed43b47c9d22b36bdffa46a275faa82fec4793dc77ed5e83-Screenshot_2024-10-08_at_2.22.25_PM.png)\
        It’s important to remember to copy only the ID and not the entire URL.
    * Private Key: This will be the value generated in your JSON file where the parameter name will be private\_key. Important note: you should copy everything that is in the line for this value except the quotation marks ""
    * Client Email: This will be the value generated in your JSON file where the parameter name will be client\_email
    * Now in your Botpress Studio
    * Select the integration tab as shown in the image below\
        ![Screenshot 2024-10-09 at 9.21.25 AM.png](https://files.readme.io/8a1834a2eb43894281b15ac3412a4f25b1fd0a97baf255778ae4841dfcca9122-Screenshot_2024-11-08_at_1.38.27_PM.png)
    * Search for Sheet and install the integration  ![Screenshot 2024-10-09 at 9.24.00 AM.png](https://files.readme.io/8f50e7b45c28124a96cf7facf309c46fe1e42691c012ec53f4b96a3e037b848b-Screenshot_2024-11-08_at_1.48.37_PM.png)
    * Private Key: This will be the value generated in your JSON file where the parameter name will be private\_key. Important note: you should copy everything that is in the line for this value except the quotation marks ""
    * Client Email: This will be the value generated in your JSON file where the parameter name will be client\_email
    * After everything is done, just save the settings and your bot is integrated with Google Sheet
