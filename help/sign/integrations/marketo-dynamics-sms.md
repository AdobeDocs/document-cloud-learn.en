---
title: SMS notifications for Adobe Sign for Microsoft Dynamics agreements
description: Learn how to send a text message, email, or push notification to let the signer know an agreement is on it's way
role: Administrator
product: Adobe Sign
solution: Document Cloud
level: Intermediate
topic: Integrations
---

# SMS notifications for Adobe Sign for Microsoft Dynamics agreements

When you create an Adobe Sign agreement, it may be useful to send a text message, email, or push notification to let the signer know it's on its way. Here we'll go over an example of sending an SMS notification using Twilio. In order to send an SMS from Marketo, you must have purchased an SMS management feature. There are other Marketo SMS solutions to choose from, but the example here is for Twilio SMS. More information about purchasing and configuring Twilio SMS can be found [here.](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)

## For agreements created using Microsoft Dynamics 365

Before continuing with the creation of the campaign program, ensure you have the Marketo and Microsoft Dynamics sync installed. Information about Microsoft Dynamics sync is available [here.](https://docs.marketo.com/display/public/DOCS/Microsoft+Dynamics+Sync)

You will also need to install Adobe Sign for Microsoft Dynamics 365 if you haven't already. Information about this plugin is available [here.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

### Finding the Custom Object

If the *Marketo - Dynamics Sync* and *Adobe Sign for Dynamics* configuration was done correctly, two new options for Dynamics will appear in the Marketo Admin Terminal.

![Admin](assets/adminTerminal.png)

1. Click on **Dynamics Entities Sync**. Sync must be disabled before syncing custom entities. If this is your first time, click **Sync Schema**. Otherwise, click **Refresh Schema** to ensure you have the latest.

    ![Refresh](assets/refreshSchema.png)

### Syncing the Custom Object

On the right side, you will see Lead, Contact, and Account-based Custom Objects. These are Custom Objects that can be synced from Dynamics, and they each have the same child objects. 

If you want to trigger when a Lead is added to an agreement in Dynamics, Enable Sync for the objects under Lead. 

If you want to trigger when a Contact is added to an agreement Dynamics, Enable Sync for the objects under Contact. 

If you want to trigger when an Account is added to an agreement in Dynamics, Enable Sync for the objects under Account.

1. **Enable Sync** for the Agreement object below, *under the desired Parent (Lead, Contact, or Account)*.

    ![Custom Objects](assets/enableSyncDynamics.png)

1. A new window will open up with the fields under Agreement that you can sync. I recommend selecting every property just in case. Be sure to also tick the boxes under **Constraint** and **Trigger** to expose them to your Marketing Activities.

    ![Custom Sync 1](assets/entitySync1.png)

    ![Custom Sync 2](assets/entitySync2.png)

1. When you're finished enabling sync on the Custom Objects, remember to reactivate the Sync. Go back to the Admin Terminal. Click on **Microsoft Dynamics**. Then, click on **Enable Sync**.

    ![Microsoft Dynamics](assets/microsoftDynamics.png)

    ![Enable Global](assets/enableGlobalDynamics.png Create the Program

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

    If the configuration for the Custom Object Sync was done correctly, you should see several triggers available for use under the Microsoft folder. 

1. Click and drag *Added to Agreement* to the Smart List, and add any constraints you wish to have on the trigger.

    ![Added to Agreement](assets/addedToAgreementDynamics.png)

### Setting up the Smart Campaign Flow

The next step is to call the webhook whenever the Trigger goes off.

1. Click on the **Flow** tab in the Smart Campaign. Search for and drag the **Call Webhook** flow onto the canvas and select the webhook you created in the previous section.

    ![Call Webhook](assets/callWebhook.png)

Congratulations! You've now set up an SMS notice campaign for leads who are added to an agreement.