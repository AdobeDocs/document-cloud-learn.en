---
title: Sending reminders for unsigned Adobe Sign for Microsoft Dynamics 365 agreements
description: Learn how to send a text message, email, push notification, or SMS reminder if it remains unsigned
role: Administrator
product: Adobe Sign
solution: Document Cloud
level: Intermediate
topic: Integrations
---

# Sending reminders for unsigned Adobe Sign for Microsoft Dynamics 365 agreements

When you create an Adobe Sign agreement, it may be useful to send an email, push notification, or SMS reminder if it remains unsigned after a period of time. Here we'll go over an example of sending an email reminder for unsigned Agreements.

## For agreements created using Microsoft Dynamics 365

Before continuing with the creation of the campaign program, ensure you have the Marketo and Microsoft Dynamics sync installed. Information about Microsoft Dynamics sync is available [here.](https://docs.marketo.com/display/public/DOCS/Microsoft+Dynamics+Sync)

You will also need to install [Adobe Sign for Microsoft Dynamics 365](https://appsource.microsoft.com/en-us/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86) if you haven't already. Information about this plugin is available [here.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

### Finding the Custom Object

If the *Marketo - Dynamics Sync* and *Adobe Sign for Dynamics* configuration was done correctly, two new options for Dynamics will appear in the Marketo Admin Terminal.

![Admin](assets/adminTerminal.png)

1. Click on **Dynamics Entities Sync**. Sync must be disabled before syncing custom entities. If this is your first time, click **Sync Schema**. Otherwise, click **Refresh Schema** to ensure you have the latest.

    ![Refresh](assets/refreshSchema.png)

### Syncing the Custom Object

On the right side, you will see Lead, Contact, and Account-based Custom Objects. These are Custom Objects that can be synced from Dynamics, and they each have the same child objects. 

If you want to send a reminder when a Lead has not signed an agreement in Dynamics, Enable Sync for the objects under Lead. 

If you want to send a reminder when a Contact has not signed an agreement in Dynamics, Enable Sync for the objects under Contact. 

If you want to send a reminder when an Account has not signed an agreement in Dynamics, Enable Sync for the objects under Account.

1. **Enable Sync** for the agreement object below, under the desired Parent (Lead, Contact, or Account)*.

    ![Custom Objects](assets/enableSyncDynamics.png)

1. A new window will open with the fields under Agreement that you can sync. I recommend selecting every property just in case. Be sure to also tick the boxes under **Constraint** and **Trigger** to expose them to your Marketing Activities.

    ![Custom Sync 1](assets/entitySync1.png)

    ![Custom Sync 2](assets/entitySync2.png)

1. When you're finished enabling sync on the Custom Objects, remember to reactivate the Sync. Go back to the Admin Terminal. Click on **Microsoft Dynamics**. Then, click on **Enable Sync**.

    ![Microsoft Dynamics](assets/microsoftDynamics.png)

    ![Enable Global](assets/enableGlobalDynamics.png)

### Create the Program and Token

Let's create a program to store all the things we need for our agreement reminder campaign. We'll also learn how to create custom tokens for Adobe Sign data, so we can include the relevant data in the email. In this case, our relevant data is the Name and Current Signer URL.

1. In the Marketing Activities section of Marketo, right-click on Marketing Activities on the left bar, select **New Campaign Folder**, and give it a name.

    ![New Folder](assets/newFolder.png)

1. Right-click on the folder you just created, select **New Program**, and give it a name. Leave everything else as default, then click **Create**.

    ![New Program 1](assets/newProgram1.png)

    ![New Program 2](assets/newProgram2.png)

1. Click on **My Tokens**, then drag **Email Script** over to the canvas.

    ![Email Script](assets/emailScript.png)

1. Give it a name, then click on **Click to Edit**.

    ![Name and Edit](assets/nameAndSave.png)

1. Expand **Custom Objects** on the right-hand side, then expand the **Agreement** object. Find and drag *Name*, *Agreement Status*, *Sent on*, and *Current Signer Url* onto the canvas.

1. Write a Velocity script using these tokens to display the agreement URL that goes unsigned for a week. This will be matched by our Campaign filter later on. There are many ways to do this, but here is an example that compares the current date to *Sent On*: 

    ```
    #foreach($agreement in $adobe_agreementList)
        #if($agreement.adobe_esagreementstatus == "Out for Signature")
            #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
            #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.adobe_datesent)) )
            #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
            
            #if($dateDiff >= 7)
                #set($agreementName = $agreement.adobe_name)
                #set($agreementURL = $agreement.adobe_currentsignerurl.substring(8))
                #break
            #else
            #end
        #else
        #end
    #end

    #if(${agreementName})
        <a href="https://${agreementURL}">${agreementName}</a>
    #else
        Please contact us. 
    #end
    ``` 

When you're finished, click **Save**.

### Create the Reminder

When sending a reminder for an Adobe Sign agreement, it is a good idea to include some personalization. The name of the signer, the name of the agreement, and a link to the agreement would make for an effective reminder. We'll leave the styling of the email up to you, but here's how to set up the personalization.

1. Right-click on the Program you created and click **New Local Asset**, then select **Email**.

    ![New Email](assets/createNewEmail.png)

1. A new tab will open with the Template Picker. For simplicity in this example, we'll use a Personal Note. Enter a **Name** and **Description** for the email, select a template, and click **Create**.

    ![Template Picker](assets/templatePicker.png)

1. Set the **From Name** and **From Address**. The template should have First Name personalization in-place.

    ![Reminder Email](assets/reminderEmail.png)

1. Click on the message body to bring up the Editor. Click on the **Insert Token** button, find the custom Agreement URL token you created, and click **Insert**. Finish customizing your email, then click **Save**.

    ![Insert Token](assets/insertToken.png)

1. Preview using a profile you know has an agreement assigned to it. If everything was done correctly, you should see a link to the URL with the Agreement Name as the label. Good job! Now your reminder email is incredibly powerful.

    ![Email Link](assets/emailLink.png)

### Setting up the Smart Campaign Filter

The next step in creating a Campaign Action is defining the Filter. 

1. Right-click on the Program you created, and click **New Smart Campaign**.

    ![Smart Campaign 1](assets/smartCampaign1.png)

1. Give it a name of your choosing, then click **Create**.

    ![Smart Campaign 2](assets/smartCampaign2.png)

1. If the configuration for the Custom Object Sync was done correctly, you should see the following filters available for use under the Microsoft folder. Search for, then click and drag **Has Agreement** to the Smart List.

    ![Has Agreement](assets/hasAgreementDynamics1.png)

1. The fields you exposed to the Trigger should now be available in **Add Constraint**. Select **Agreement Status** and any other fields you wish to filter by. For each field you add, be sure to define the values to filter by. In this case, it will only trigger when the **Agreement Status** is *Out for Signature* and **Sent On** is *in past before 1 week*. 

    ![Agreement Status](assets/hasAgreementDynaSentOn.png)

    >[!NOTE]
    >
    > Make sure to add a unique identifier to the constraints, like **Name**, if you want this campaign to only run for certain agreements.

1. You've now found every Lead who has been sent an agreement that has not been signed in a week. You can confirm the Campaign audience and see who will qualify in the Schedule tab.

    ![Qualifiers](assets/qualifiers.png)

### Setting up the Smart Campaign Flow

Since we leveraged the use of the **Days Until Expires** field in the Campaign filter, we can keep our Campaign flow simple and use a scheduled recurrence for the Campaign.

1. Click on the **Flow** tab in the Smart Campaign. Search for and drag the **Send Email** flow onto the canvas and select the reminder email you created in the previous section.

    ![Send Email](assets/sendEmail.png)

1. Click on the **Schedule** tab in the Smart Campaign. Ensure that in the **Smart Campaign Settings**, the campaign flow is limited to only run once per person (unless spamming your customers once a week is the goal!). Then, click on the **Schedule Recurrence** tab.

    ![Schedule Tab](assets/scheduleTab.png)

1. Set the **Schedule** to *Daily*, choose a start day and time and an end date for the Campaign if necessary.

    ![Schedule Settings](assets/scheduleSettings.png)

Congratulations! You have set up a reminder campaign for unsigned agreements. Once an unsigned agreement is a week from expiring, the signer will qualify for our Campaign. Since we have a daily scheduled recurrence set up for the Campaign, every day at 1:00 PM, we will send a reminder to the qualifiers. Because we set the Smart Campaign Settings to once per person, this flow will only happen once per person, on the 7th day the agreement goes unsigned.

In other words: customers who have not signed an agreement will be sent an email reminder one week before it expires.





