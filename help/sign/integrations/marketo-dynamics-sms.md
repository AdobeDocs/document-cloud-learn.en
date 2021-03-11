---
title: Send notifications using Adobe Sign for Microsoft Dynamics 365 and Marketo
description: Learn how to send a text message, email, or push notification to let the signer know an agreement is on its way
role: Administrator
product: Adobe Sign
solution: Document Cloud
level: Intermediate
topic: Integrations
thumbnail: KT-7249.jpg
---

# Send notifications using Adobe Sign for Microsoft Dynamics 365 and Marketo

Learn how to send a text message, email, or push notification to let the signer know an agreement is on its way using Adobe Sign for Microsoft Dynamics 365 and Marketo. To send notifications from Marketo, you first need to purchase or configure a Marketo SMS management feature. This walkthrough uses [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), but there are other Marketo SMS solutions available.

## Prerequisites

1. Install the Marketo and Microsoft Dynamics sync. Information about Microsoft Dynamics sync is available [here.](https://docs.marketo.com/display/public/DOCS/Microsoft+Dynamics+Sync)

1. Install Adobe Sign for Microsoft Dynamics 365. Information about this plugin is available [here.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Find the custom object

Once the Marketo - Dynamics Sync and Adobe Sign for Dynamics configurations are complete, two new options will appear for Dynamics in the Marketo Admin Terminal.

![Admin](assets/adminTerminal.png)

1. Click on **Dynamics Entities Sync**. Sync must be disabled before syncing custom entities. Click **Sync Schema** if this is your first time. Otherwise, click **Refresh Schema**.

    ![Refresh](assets/refreshSchema.png)

## Sync the custom object

On the right side, see Lead, Contact, and Account-based custom objects. 

**Enable Sync** for the objects under Lead if you want to trigger when a Lead is added to an agreement in Dynamics. 

**Enable Sync** for the objects under Contact if you want to trigger when a Contact is added to an agreement in Dynamics.

**Enable Sync** for the objects under Account if you want to trigger when an Account is added to an agreement in Dynamics.

1. **Enable Sync** for the Agreement object under the desired Parent (Lead, Contact, or Account).

    ![Custom Objects](assets/enableSyncDynamics.png)

1. In the new window, select the properties you want under Agreement. Then tick the boxes under **Constraint** and **Trigger** to expose them to your Marketing Activities.

    ![Custom Sync 1](assets/entitySync1.png)

    ![Custom Sync 2](assets/entitySync2.png)

1. Reactivate the sync after enabling sync on the custom objects. Go back to the Admin Terminal, click **Microsoft Dynamics**, then click on **Enable Sync**.

    ![Microsoft Dynamics](assets/microsoftDynamics.png)

    ![Enable Global](assets/enableGlobalDynamics.png)

## Create the program

1. In the Marketing Activities section of Marketo, right-click on **Marketing Activities** on the left bar, select **New Campaign Folder**, and give it a name.

    ![New Folder](assets/newFolder.png)

1. Right-click on the created folder, select **New Program**, and give it a name. Leave everything else as default, then click **Create**.

    ![New Program 1](assets/newProgram1.png)

    ![New Program 2](assets/newProgram2.png)

## Set up Twilio SMS

First ensure you have an active Twilio account and purchased the SMS features you require. 

Setting up the Marketo - Twilio SMS webhook requires three Twilio parameters from your account.

- Account SID
- Account Token
- Twilio Phone Number

Retrieve these parameters from your account, now open your Marketo instance.

1. Click on **Admin** in the top right.

    ![Admin](assets/adminTab.png)

1. Click on **Webhooks**, then **New Webhook**.

    ![Webhooks](assets/webhooks.png)

1. Enter a **Webhook Name** and **Description**.

1. Enter the following URL and be sure to replace the **[ACCOUNT_SID]** and **[AUTH_TOKEN]** with your Twilio credentials.
 
    ```
    https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
    ```

1. Select **POST** as your Request type.

1. Enter the following **Template** and be sure to replace **[MY_TWILIO_NUMBER]** with your Twilio phone number and **[YOUR_MESSAGE]** with a message of your choosing.

    ```
    From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
    ```

1. Set the Request Token Encoding to Form/URL.

1. Set the Response type to JSON then click **Save**.

## Set up the Smart Campaign Trigger

1. In the Marketing Activities section, right-click on the program you created, then select **New Smart Campaign**.

    ![Smart Campaign 1](assets/smartCampaign1.png)

1. Name it, then click **Create**.

    ![Smart Campaign 2](assets/smartCampaign3.png)

    You should see several triggers available for use under the Microsoft folder. 

1. Click and drag Added to Agreement to the Smart List. Add any constraints you wish to have on the trigger.

    ![Added to Agreement](assets/addedToAgreementDynamics.png)

## Set up the Smart Campaign Flow

1. Click on the **Flow** tab in the Smart Campaign. Search for and drag the **Call Webhook** flow onto the canvas and select the webhook you created in the previous section.

    ![Call Webhook](assets/callWebhook.png)

1. Your SMS notice campaign for leads who are added to an agreement is now set up. 