---
title: SMS notifications for Adobe Sign for Salesforce agreements
description: Learn how to send a text message, email, or push notification to let the signer know an agreement is on it's way
role: Administrator
product: Adobe Sign
solution: Document Cloud
level: Intermediate
topic: Integrations
---

# SMS notifications for Adobe Sign for Salesforce agreements

When you create an Adobe Sign agreement, it may be useful to send a text message, email, or push notification to let the signer know it's on its way. Here we'll go over an example of sending an SMS notification using Twilio. In order to send an SMS from Marketo, you must have purchased an SMS management feature. There are other Marketo SMS solutions to choose from, but the example here is for Twilio SMS. More information about purchasing and configuring Twilio SMS can be found [here.](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)

## For agreements created using Salesforce

Before continuing with the creation of the campaign program, ensure you have the Marketo and Salesforce sync installed. Information about Salesforce sync installation is available [here.](https://docs.marketo.com/display/public/DOCS/Salesforce+Sync)

You will also need to install *Adobe Sign for Salesforce* if you haven't already. Information about this plugin is available [here.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

### Finding the Custom Object

If the *Marketo - Salesforce Sync* and *Adobe Sign for Salesforce* configuration was done correctly, several new options for Salesforce will appear in the Marketo Admin Terminal.

![Admin](assets/adminTab.png)

![Object Sync](assets/salesforceAdmin.png)

1. If this is your first Custom Object, click **Sync Schema**. Otherwise, click **Refresh Schema** to ensure you have the latest.

    ![Refresh](assets/refreshSchema1.png)

1. If your global sync is running, you will have to disable it by clicking **Disable Global Sync**.

    ![Disable](assets/disableGlobal.png)

1. Click **Refresh Schema**.

    ![Refresh 2](assets/refreshSchema2.png)

### Syncing the Custom Object

On the right side, you will see Lead, Contact, and Account-based Custom Objects. These are Custom Objects that can be synced from Salesforce, and they each have the same child objects. 

If you want to trigger when a Lead is added to an agreement in Salesforce, Enable Sync for the objects under Lead. 

If you want to trigger when a Contact is added to an agreement in Salesforce, Enable Sync for the objects under Contact. 

If you want to trigger when an Account is added to an agreement in Salesforce, Enable Sync for the objects under Account.

1. **Enable Sync** for the Custom Objects shown below, *under the desired Parent (Lead, Contact, or Account)*.

    ![Custom Objects](assets/customObjects.png)

1. The following assets show how to **Enable Sync**.

    ![Custom Sync 1](assets/customObjectSync1.png)

    ![Custom Sync 2](assets/customObjectSync2.png)

1. When you're finished enabling sync on the Custom Objects, remember to reactivate the Sync:

![Enable Global](assets/enableGlobal.png)

#### Create the Program

Let's create a program to store all the things we need for our agreement notification campaign.

1. In the Marketing Activities section of Marketo, right-click on Marketing Activities on the left bar, select **New Campaign Folder**, and give it a name.

    ![New Folder](assets/newFolder.png)

1. Right-click on the folder you just created, select **New Program**, and give it a name. Leave everything else as default, then click **Create**.

    ![New Program 1](assets/newProgram1.png)

    ![New Program 2](assets/newProgram2.png)

### Setting up Twilio SMS

Here we will assume you have an active Twilio account and have purchased the SMS features you require. 

The first step to setting up the Marketo - Twilio SMS webhook requires you to grab 3 Twilio parameters from your account.

- Account SID
- Account Token
- Twilio Phone Number

Once you have retrieved these three parameters from your account, open up your Marketo instance.

1. Click on **Admin** in the top right.

    ![Admin](assets/adminTab.png)

1. Click on **Webhooks**, then **New Webhook**.

    ![Webhooks](assets/webhooks.png)

1. Enter a **Webhook Name** and **Description**.

1. Enter the following **URL** and be sure to replace the **[ACCOUNT_SID]** and **[AUTH_TOKEN]** with your Twilio credentials.

    ```
    https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
    ```

1. Select **POST** as your Request type.

1. Enter the following **Template** and be sure to replace **[MY_TWILIO_NUMBER]** with your Twilio phone number and **[YOUR_MESSAGE]** with a message of your choosing.

    ```
    From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
    ```

1. Set the Request Token Encoding to **Form/URL**.

1. Set the Response type to **JSON**, then click **Save**.

### Setting up the Smart Campaign Trigger

The first step for creating a Campaign Action is defining the Trigger. 

1. In the Marketing Activities section, right-click on the Program you created, and select **New Smart Campaign**.

    ![Smart Campaign 1](assets/smartCampaign1.png)

1. Give it a name of your choosing, then click **Create**.

    ![Smart Campaign 2](assets/smartCampaign3.png)

    If the configuration for the Custom Object Sync was done correctly, you should see the following triggers available for use under the Salesforce folder. 

1. Click and drag *Added to Agreement* to the Smart List, and add any constraints you wish to have on the trigger.

    ![Added to Agreement 2](assets/addedToAgreement2.png)

### Setting up the Smart Campaign Flow

The next step is to call the webhook whenever the Trigger goes off.

1. Click on the **Flow** tab in the Smart Campaign. Search for and drag the **Call Webhook** flow onto the canvas and select the webhook you created in the previous section.

    ![Call Webhook](assets/callWebhook.png)

Congratulations! You've now set up an SMS notice campaign for leads who are added to an agreement.