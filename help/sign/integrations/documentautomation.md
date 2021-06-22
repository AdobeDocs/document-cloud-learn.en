---
title: Document Automation with Adobe Sign for Microsoft Power Platform
description: Learn how to activate and use the Adobe Sign and Adobe PDF Tools connectors for Microsoft Power Apps. Build workflows that automate business approval and signature processes quickly and securely without any code
role: Business Practitioner, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7488.jpg
kt: 7488
exl-id: 4113bc3f-293c-44a8-94ab-e1dbac74caed
---
# Document automation with Adobe Sign for Microsoft Power Platform

Learn how to activate and use the Adobe Sign and Adobe PDF Tools connectors for Microsoft Power Apps. Build workflows that automate business approval and signature processes quickly and securely without any code. There are four parts to this hands-on tutorial outlined in the links below:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="documentautomation.md#part1">
        <img alt="Part 1: Store signed agreement in SharePoint with Adobe Sign" src="assets/documentautomation/AutomationPart1_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part1"><strong>Part 1: Store signed agreement in SharePoint with Adobe Sign</strong></a>
    </div>
  </td>
  <td>
    <a href="documentautomation.md#part2">
        <img alt="Part 2: Automated approval process to get e-signature with Adobe Sign" src="assets/documentautomation/AutomationPart2_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part2"><strong>Part 2: Automated approval process to get e-signature with Adobe Sign</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part3">
      <img alt="Part 3: Automated document OCR with Adobe PDF Tools" src="assets/documentautomation/AutomationPart3_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part3"><strong>Part 3: Automated document OCR with Adobe PDF Tools</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part4">
      <img alt="Part 4: Automated document assembly with Adobe PDF Tools" src="assets/documentautomation/AutomationPart4_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part4"><strong>Part 4: Automated document assembly with Adobe PDF Tools</strong></a>
    </div>
  </td>
</tr>
</table>

## Prerequisites

* Microsoft 365 and Power Automate familiarity
* Adobe Sign knowledge
* Microsoft 365 account with access to SharePoint and Power Automate (Basic for Adobe Sign, Premium for Adobe PDF Tools)
* Adobe Sign for enterprise or Adobe Sign developer account

**Exercises 1 and 2**

* Adobe Sign account with access to the API. A developer account or an Enterprise account.
* SharePoint site accessible by Power Automate that you have edit permissions to. Full admin access is recommended.
* Sample document for the Signature approval request and signing.

**Exercises 3 and 4**

Download materials [here](https://github.com/benvanderberg/adobe-sign-pdftools-powerautomate-tutorial)

## Part 1: Store signed agreement in SharePoint with Adobe Sign {#part1}

In part one, you'll use a Power Automate Flow template to set up an automated workflow that will save all signed agreements to your SharePoint Site.

1. Navigate to Power Automate.
1. Search for Adobe Sign.

   ![Screenshot of navigating to Power Automate](assets/documentautomation/automation_1.png)
   
1. Choose **Save an Adobe Sign completed agreement to SharePoint library**.

   ![Screenshot of Save an Adobe Sign completed agreement to SharePoint library action](assets/documentautomation/automation_2.png)

1. Review the screen and configure any needed connections. Enable the Adobe Sign connection.
1. Click the blue `+` symbol.

   ![Screenshot of Adobe Sign and SharePoint flow connection](assets/documentautomation/automation_3.png)

1. Enter your Adobe Sign account email and click the password field in the new window.

   ![Screenshot of Adobe Sign sign in screen](assets/documentautomation/automation_4.png)

   Wait a moment for Adobe to check your account.

   >[!NOTE]
   >
   >This check will route you to the appropriate login if you are using an Adobe ID or our corporate SSO.

1. Complete login.
1. Click **Continue** to go to the Flow editing screen.
1. Name the trigger.

   ![Screenshot of naming the trigger](assets/documentautomation/automation_5.png)

1. Configure your SharePoint settings.

   ![Screenshot of configuring your SharePoint settings](assets/documentautomation/automation_6.png)

   **Site Address:** Your SharePoint Site
   **Folder Path:** Path to the Shared Documents you want to use
   **File Name:** Accept the default
   **File Content:** Accept the default

1. Save the flow.

   ![Screenshot of the Save icon](assets/documentautomation/automation_7.png)

1. Navigate to the flow overview screen with the blue back arrow. You will test this flow in part 2.

   ![Screenshot of the flow overview screen](assets/documentautomation/automation_8.png)

You will test this flow in the next part.

## Part 2: Automated approval process to get e-signature with Adobe Sign {#part2}

In part two, we build off the first part with a more robust Flow and test both Flows to see them in action.

1. Select **Templates** on the left side from the Power Automate interface.

   ![Screenshot of selecting Templates](assets/documentautomation/automation_9.png)

1. Search for “manager approval.”
1. Select **Request manager approval for a selected file**.

   ![Screenshot of selecting Request manager approval for a selected file](assets/documentautomation/automation_10.png)

   Review the connections and add any you are missing.

   >[!NOTE]
   >
   >If this is the first flow you are doing with approvals, they will be fully configured when the flow runs.

1. Click **Continue** to go to the flow editing screen.

   This flow has a lot of pre-configured steps including error checking and nested conditional steps.

1. Configure **For a selected file** as follows:
   **Site Address:** Your SharePoint site
   **Library Name:** Your Documents repository
1. Add an input as follows:
   **Type**: Email
   **Name**: Signer Email

   ![Screenshot of configuring the flow](assets/documentautomation/automation_11.png)

1. Configure **Get File Properties:** as follows:
   **Site Address:** Your SharePoint site
   **Library Name:** Your Documents repository

1. Scroll down and look for **If yes**.

   ![Screenshot of If yes configuration](assets/documentautomation/automation_12.png)

1. Click **Add an action** in the **If yes** box (not the bottom most one) to add the steps to send for signature.

   ![Screenshot of adding an action in the If yes box](assets/documentautomation/automation_13.png)

1. Search for **SharePoint get file content** and choose **Get file content**.

   ![Screenshot of the search box](assets/documentautomation/automation_14.png)

1. Configure the **Get file content** as follows:
   
   ![Screenshot of the Get file content configuration](assets/documentautomation/automation_15.png)

   **Site Address:** Your SharePoint site.
   **File Identifier:** Search for “identifier,” and choose Identifier from the **Get file properties** step.
1. Search for “Adobe” and choose **Adobe Sign** to add another action.

   ![Screenshot of search menu](assets/documentautomation/automation_16.png)

1. Enter “upload” into the search box for Adobe Sign and select **Upload a document and get a document ID**.
1. Search for the dynamic variable **Name** to get the name of the item/document selected in the trigger under **File Name**.
1. Click **Expression** in the variable assistant under **File Content**.

   ![Screenshot of Upload a document and get a document ID screen](assets/documentautomation/automation_17.png)

1. Add a single apostrophe, then click back to **Dynamic Content**, delete your apostrophe, select **File Content** and then click **OK**.

   Make sure there are no additional apostrophes and it looks like the sample below.

   ![Screenshot of what the Dynamic Content screen should look like](assets/documentautomation/automation_18.png)

1. Search for “create” in the Adobe Sign search area to add another Adobe Sign action.
1. Select **Create and agreement from an uploaded document and send for signature**.

   ![Screenshot of searching for create](assets/documentautomation/automation_19.png)

1. Configure the required information:
   Choose **Name** from the dynamic variable assistant in **Agreement Name**. 
   Choose **Document ID** from the dynamic variable assistant in **Document ID**.
   Choose **Signer Email** from the dynamic variable assistant in **Participant Email**.
   Enter “1” in **Participant Order**.
   Choose **Signer** from dropdown in **Participant Role**.

   ![Screenshot of the required information](assets/documentautomation/automation_20.png)

1. **Save** the Flow.

### Test the flow

Go to your SharePoint site’s document repository to test it out.

1. Select the document and choose **Automate** and the **Flow** you just created.

   ![Screenshot of selecting the Automate menu and flow](assets/documentautomation/automation_21.png)

1. Start the flow to validate the connections (first run of flow only).
1. Enter a nice message to the approver in **Message**.
1. Enter email for the document Signer in **Signer Email**.
1. Click **Run flow**.

The configured approver for the user starting the flow will get an approval request. You can approve through email or through the Power Automate Action Items menu. 
Once approved, sign your document. Depending on your user and if they are logged into Sign, you may need to open the signing windows in a private browser window.

![Screenshot of opening in private browser window](assets/documentautomation/automation_22.png)

Complete the signing, and then look back in your SharePoint folder.

![Screenshot of SharePoint folder](assets/documentautomation/automation_23.png)

## Part 3: Automated document OCR with Adobe PDF Tools {#part3}

In part three, you'll learn how to automate OCR in PDFs when they are imported into Microsoft SharePoint. This addresses an issue that occurs with scanned PDF documents that are not searchable in SharePoint.

![Screenshot of PDF document in browser](assets/documentautomation/automation_24.png)

### Setup a folder in SharePoint

Go to Microsoft SharePoint where you would like to store documents.

1. Click **+ New** to create a new folder called “Processed Contracts.”
1. Click **+ New** to create a new folder called “Old Contracts.”

   ![Screenshot of new folders](assets/documentautomation/automation_25.png)

These folders are now referenced as part of your Power Automate flow.

### Create a flow from a template

1. Log in to https://flow.microsoft.com.
1. Click **Templates** in the sidebar.

   ![Screenshot of selecting templates](assets/documentautomation/automation_26.png)

1. Select **Convert newly added files to text searchable PDF in SharePoint**.
1. Click the **+** symbol next to Adobe PDF Tools.

   ![Screenshot of selecting the + symbol](assets/documentautomation/automation_27.png)

1. Navigate to https://www.adobe.com/go/powerautomate_getstarted in a new tab.
1. Click **Get Started**.

   ![Screenshot of Get Started button](assets/documentautomation/automation_28.png)

1. Sign in with your Adobe ID.

   ![Screenshot of the Sign in screen](assets/documentautomation/automation_29.png)

1. Enter Credentials Name and Credentials Description and click **Create Credentials**.

   ![Screenshot of the Create Credentials screen](assets/documentautomation/automation_30.png)

   Keep the window with the credentials open. You will need to enter them into Microsoft Power Automate.

   ![Screenshot of the browser tab to keep open](assets/documentautomation/automation_31.png)

1. Enter the credentials and click **Create in Microsoft Power Automate**.

   ![Screenshot of entering the PDF Tools credentials](assets/documentautomation/automation_32.png)

1. Click **Continue**.

   ![Screenshot of where to click Continue](assets/documentautomation/automation_33.png)

   Now you can see a view of the workflow, and you'll need to configure it for your environment.

1. Select Site Address field and choose which SharePoint site you are using under the trigger called **When a file is created in a folder**.

   ![Screenshot of selecting When a file is created in a folder trigger](assets/documentautomation/automation_34.png)

1. Click the folder icon to navigate to the Old Contracts folder located under Folder ID.

   ![Screenshot of selecting Old Contracts folder](assets/documentautomation/automation_35.png)

1. Edit the **Create file** action at the bottom of the flow:

   Change **Site Address** to your site address.
   Specify the location of the Processed Contracts folder in the Folder Path.

1. Click **Save** in the top right corner.
1. Click **Test**. 
1. Select **Manually**.
1. Click **Test**.

   ![Screenshot of the Test flow](assets/documentautomation/automation_36.png)

### Try your new flow

1. Navigate to the Old Contracts folder in SharePoint.
1. Navigate into E03/Old Contracts in the exercise files you downloaded.
1. Copy the ReleaseFormXX.pdf files into the Old Contracts folder in SharePoint.

   ![Screenshot of copying the files](assets/documentautomation/automation_37.png)

Now if you navigate to the Processed Contracts folder, you can see your PDFs available after the flow is given a few moments to run. If you open the PDFs, you can see that the text is selectable.
In addition, SharePoint indexes the document, allowing you to search the content of your documents from the search bar in SharePoint.

## Part 4: Automated document assembly with Adobe PDF Tools {#part4}

In part four, you'll learn how to merge many documents together based on information provided while selecting and starting a flow from Microsoft SharePoint. In this scenario, the flow will:

* Ask for information to choose what to include in a package for a customer.
* Based on the information provided, it merges many documents together. These documents include a cover page and optional whitepapers.
* The merged document is saved to SharePoint.

### Import exercise files into SharePoint

1. Open the E04 folder in the Exercise files.
1. Import the Proposal, Templates, and Generated Docs folders into SharePoint.

   ![Screenshot of importing folders](assets/documentautomation/automation_38.png)

These folders will be used for reference. In particular, you will use the Proposal.docx file for your proposal. 

In the Templates folder, there is a Covers folder that includes cover page designs for different cities. There is also a Whitepapers folder that contains optional additional whitepapers that will be attached to the end if selected.

### Import the flow into Microsoft Power Automate

1. Log in to Microsoft Power Automate (https://flow.microsoft.com).
1. Click **My Flows**.

   ![Screenshot of where to select My Flows](assets/documentautomation/automation_39.png)

1. Click **Import**.

   ![Screenshot of import screen](assets/documentautomation/automation_40.png)

1. Click **Upload** and choose the GenerateProposal_20210311231623.zip folder in E04/Flows/.

   ![Screenshot of selecting folder](assets/documentautomation/automation_41.png)

1. Click **Import**.

1. Click the Wrench icon under Action next to **Send Proposal to Customer**.

   ![Screenshot of the wrench icon](assets/documentautomation/automation_42.png)

1. Select **Create as new** under Setup.
1. Set the name of the flow under Resource Name.
1. Click **Save**.

   Repeat this for the other Related resources and select your connection.

   ![Screenshot of saving the file](assets/documentautomation/automation_43.png)

1. Click **Import** after you have made all your connections.

### Set For a selected file

Now that the flow is created, do the following:

1. Click **Edit**.

   ![Screenshot of where to select edit](assets/documentautomation/automation_44.png)

1. Select the trigger **For a selected file**.

   Add your SharePoint site in the Site Address.
   Add your Library in Library.

   ![Screenshot of completed trigger](assets/documentautomation/automation_45.png)

### Set templateFolderPath

1. Click the templateFolderPath variable.
1. Set the path to where the Templates folder is located inside the SharePoint site that you imported.

### Set Cover Get File Content

1. Click **Cover** action, which expands the Scope.
1. Expand **Cover: Get File Content**.

   Set Site Address to your SharePoint site.

   ![Screenshot of expanded Cover](assets/documentautomation/automation_46.png)



### Set Selected File

1. Expand the **Selected File** scope action.

   Change the Site Address and Library Name to your SharePoint site and Library respectively under **Get file properties**.
   Change the Site Address to your SharePoint site under **Get file content**.

   ![Screenshot of expanded Selected File action](assets/documentautomation/automation_47.png)

### Set Whitepapers

1. Click **Whitepapers** action.
1. Expand **Condition: Add Whitepaper**.

   ![Screenshot of expanded Add Whitepaper condition](assets/documentautomation/automation_48.png)

1. Expand **Whitepaper 1: Get file content using path**.
   Edit the Site Address to your specified SharePoint site.

Repeat the same steps for **Condition: Add Whitepaper 2**.

### Set Create File

1. Expand **Create File**.

   Edit Site Address and Folder Path to the SharePoint site and path where the Generated Docs folder is located.

1. Click **Save**.

### Test your flow

1. Navigate to the Proposal folder in SharePoint.
1. Select Proposal.docx folder.

   ![Screenshot of selecting proposal folder](assets/documentautomation/automation_49.png)

1. Select your flow under the **Automate** menu.

   ![Screenshot of Selecting the Automate menu](assets/documentautomation/automation_50.png)

1. Click **Continue** to begin the flow.

   ![Screenshot of Selecting the Continue button](assets/documentautomation/automation_51.png)

1. Choose your Cover and the whitepapers you want to append.
1. Click **Run flow**.

   ![Screenshot of Run flow button](assets/documentautomation/automation_52.png)

Navigate to the Generate Docs folder. You should now see your generated PDF file.

   ![Screenshot of SharePoint directory with new PDF file](assets/documentautomation/automation_53.png)

### Adding Protect and other actions to flow

Now that you have successfully created a flow, you are going to edit your flow to encrypt the PDF document with a password. This also walks through how you can utilize other actions.

1. Navigate back to the end of your flow. 
1. Click the **+** symbol between **Merge PDFs** and **Create file**.

   ![Screenshot of where to select + symbol](assets/documentautomation/automation_54.png)

1. Select **Add an action**.
1. Search for "Adobe PDF Tools".

   ![Screenshot of searching for Adobe PDF](assets/documentautomation/automation_55.png)

1. Select **Protect PDF from Viewing**.
1. Use Dynamic Content to set the File Name field to **PDF File Name from Merge PDF**.

   ![Screenshot of dynamic content](assets/documentautomation/automation_56.png)

   In the trigger, there is a Password field that is part of the initiation form. We can use that here. 

1. Search for **Password field** using Dynamic content, and place it in the Password field.

   ![Screenshot of searching for password](assets/documentautomation/automation_57.png)

1. Use Dynamic content to set it to **PDF File Content from Merge PDFs** in the File Content field.
1. Change the **Create file** to get the file content from Protect PDF rather than Merge PDFs.
1. Expand **Create file**.
1. Clear the File Content field.
1. Use Dynamic Content to place **PDF File Content** from **Protect PDF from Viewing**.

### Test your flow

1. Navigate to the Proposal folder in SharePoint.
1. Select Proposal.docx.

   ![Screenshot of selecting Proposal folder](assets/documentautomation/automation_58.png)

1. Select **Automate** to choose your flow.

   ![Screenshot of selecting Automate from the menu](assets/documentautomation/automation_59.png)

1. Click **Continue** to begin the flow.

   ![Screenshot of selecting Continue](assets/documentautomation/automation_60.png)

1. Choose the Cover and the whitepapers you want to append.
1. Set the Password field to the Password you would like to set.
1. Click **Run flow**.

   ![Screenshot of selected files and Run flow button](assets/documentautomation/automation_61.png)

1. Navigate to the Generate Docs folder.
   You should see your generated PDF file. Open the PDF file and it prompts you to enter your PDF password.

   ![Screenshot of generated PDF in SharePoint directory](assets/documentautomation/automation_62.png)
