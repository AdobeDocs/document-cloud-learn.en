---
title: Send notifications using Acrobat Sign for Microsoft Dynamics 365 and Marketo
description: Learn how to send a text message, email, or push notification to let the signer know an agreement is on its way
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo Engage, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7249
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
TQID: https://experienceleague.adobe.com/J-UO0MiY9BG6zt7UcwxYTupl00NBWNbjamrkoF-nKKE
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
  - id: c1c5fb98-9105-44ed-9df1-9e04d062a784
    internal-label: Document Cloud
feature_v2:
  - id: a1028f9a-6dbc-4a4f-adf5-eb9f85a408a6
    internal-label: Integrations
  - id: b13bd2ad-8e65-49e5-9691-2a0d31067b35
    internal-label: Integrations
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
    internal-label: Configuration
subfeature_v2:
  - id: d5c7388a-594e-4d15-9b39-98d6ce479e8b
    internal-label: Microsoft Dynamics
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
---
# Send notifications using Acrobat Sign for Microsoft Dynamics 365 and Marketo

Learn how to send a text message, email, or push notification to let the signer know an agreement is on its way using Acrobat Sign, Acrobat Sign for Microsoft Dynamic, Marketo, and the Marketo Microsoft Dynamics Sync. To send notifications from Marketo, you first need to purchase or configure a Marketo SMS management feature. This walkthrough uses [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), but other Marketo SMS solutions are available.

## Prerequisites

1. Install the Marketo Microsoft Dynamics Sync.

   Information and the latest plugin for Microsoft Dynamics Sync is available [here.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Install Acrobat Sign for Microsoft Dynamics.

    Information about this plugin is available [here.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Find the custom object

Once the Marketo Microsoft Dynamics Sync and Acrobat Sign for Dynamics configurations are complete, two new options appear in the Marketo Admin Terminal.

![Admin](assets/adminTerminal.png)

* Click **[!UICONTROL Dynamics Entities Sync]**. 

   Sync must be disabled before syncing custom entities. Click **[!UICONTROL Sync Schema]** if this is your first time. Otherwise, click **[!UICONTROL Refresh Schema]**.

   ![Refresh](assets/refreshSchema.png)

## Sync the custom object

1. On the right side, locate [!UICONTROL Lead], [!UICONTROL Contact], and [!UICONTROL Account]-based custom objects. 

    * **[!UICONTROL Enable Sync]** for the objects under Lead if you want to trigger when a Lead is added to an agreement in Dynamics. 

    * **[!UICONTROL Enable Sync]** for the objects under Contact if you want to trigger when a Contact is added to an agreement in Dynamics.

    * **[!UICONTROL Enable Sync]** for the objects under Account if you want to trigger when an Account is added to an agreement in Dynamics.

    * **Enable Sync** for the Agreement object under the desired Parent (Lead, Contact, or Account).

    ![Custom Objects](assets/enableSyncDynamics.png)

1. In the new window, select the properties you want under Agreement. 

    Enable the boxes under **[!UICONTROL Constraint]** and **[!UICONTROL Trigger]** to expose them to your Marketing Activities.

    ![Custom Sync 1](assets/entitySync1.png)

    ![Custom Sync 2](assets/entitySync2.png)

1. Reactivate the sync after enabling sync on the custom objects. 

    Go back to the [!UICONTROL Admin Terminal], then click **[!UICONTROL Microsoft Dynamics]**, then click on **[!UICONTROL Enable Sync]**.

    ![Microsoft Dynamics](assets/microsoftDynamics.png)

    ![Enable Global](assets/enableGlobalDynamics.png)

## Create the program

1. In [!UICONTROL Marketing Activities], right-click **[!UICONTROL Marketing Activities]** on the left bar, select **[!UICONTROL New Campaign Folder]**, and name it.

    ![New Folder](assets/newFolder.png)

1. Right-click on the created folder, select **[!UICONTROL New Program]**, and give it a name. 

    Leave everything else as default, then click **[!UICONTROL Create]**.

    ![New Program 1](assets/newProgram1.png)

    ![New Program 2](assets/newProgram2.png)

## Set up [!DNL Twilio] SMS

First ensure you have an active [!DNL Twilio] account and purchased the SMS features you require. 

Setting up the Marketo - [!DNL Twilio] SMS webhook requires three [!DNL Twilio] parameters from your account.

* Account SID
* Account Token
* Twilio Phone Number

Retrieve these parameters from your account, now open your Marketo instance.

1. Click **[!UICONTROL Admin]** in the top right.

    ![Admin](assets/adminTab.png)

1. Click **[!UICONTROL Webhooks]**, then click **[!UICONTROL New Webhook]**.

    ![Webhooks](assets/webhooks.png)

1. Enter a **[!UICONTROL Webhook Name]** and **[!UICONTROL Description]**.

1. Enter the following URL and be sure to replace the `ACCOUNT_SID` and `AUTH_TOKEN` with your [!DNL Twilio] credentials.
 
    ```
    https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
    ```

1. Select **[!UICONTROL POST]** as your Request type.

1. Enter the following **Template** and be sure to replace `MY_TWILIO_NUMBER` with your [!DNL Twilio] phone number and `YOUR_MESSAGE` with a message of your choosing.

    ```
    From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
    ```

1. Set the **[!UICONTROL Request Token Encoding]** to *Form/URL*.

1. Set the Response type to *JSON* then click **[!UICONTROL Save]**.

## Set up the Smart Campaign Trigger

1. In the Marketing Activities section, right-click on the program you created, then select **[!UICONTROL New Smart Campaign]**.

    ![Smart Campaign 1](assets/smartCampaign1.png)

1. Name it, then click **[!UICONTROL Create]**.

    ![Smart Campaign 2](assets/smartCampaign3.png)

    You should see several triggers available for use under the Microsoft folder. 

1. Click and drag **[!UICONTROL Added to Agreement]** to the **[!UICONTROL Smart List]**, then add any constraints you wish to have on the trigger.

    ![Added to Agreement](assets/addedToAgreementDynamics.png)

## Set up the Smart Campaign Flow

1. Click the **[!UICONTROL Flow]** tab in the [!UICONTROL Smart Campaign]. 

    Search for and drag the **Call Webhook** flow onto the canvas and select the webhook you created in the previous section.

    ![Call Webhook](assets/callWebhook.png)

1. Your SMS notice campaign for leads who are added to an agreement is now set up.
