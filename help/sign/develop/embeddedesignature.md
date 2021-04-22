---
title: Create Embedded e-Signature and Document Experiences
description: Learn how to use Adobe Sign APIs to embed e-signature and document experiences into your web platforms and content and document management systems
role: Business Practitioner, Developer
level: Intermediate
topic: Developer
thumbnail:
kt:
---
# Create embedded e-signature and document experiences

Learn how to use Adobe Sign APIs to embed e-signature and document experiences into your web platforms and content and document management systems. There are four parts to this hands-on tutorial outlined in the links below:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="embeddedesignature.md#part1">
        <img alt="Part 1: Store signed agreement in SharePoint with Adobe Sign" src="assets/embeddedesignature/EmbedPart1_thumb.jpg" />
    </a>
    <div>
    <a href="embeddedesignature.md#part1"><strong>Part 1: Store signed agreement in SharePoint with Adobe Sign</strong></a>
    </div>
  </td>
  <td>
    <a href="embeddedesignature.md#part2">
        <img alt="Part 2: Low/No Code — the power of web forms" src="assets/embeddedesignature/EmbedPart2_thumb.jpg" />
    </a>
    <div>
    <a href="embeddedesignature.md#part2"><strong>Part 2: Low/No Code — the power of web forms</strong></a>
    </div>
  </td>
  <td>
   <a href="embeddedesignature.md#part3">
      <img alt="Part 3: Send agreement with a form, merge data" src="assets/embeddedesignature/EmbedPart3_thumb.jpg" />
   </a>
    <div>
    <a href="embeddedesignature.md#part3"><strong>Part 3: Send agreement with a form and merge data</strong></a>
    </div>
  </td>
  <td>
   <a href="embeddedesignature.md#part4">
      <img alt="Part 4: Embed signing experience, redirects, and more" src="assets/embeddedesignature/EmbedPart4_thumb.jpg" />
   </a>
    <div>
    <a href="embeddedesignature.md#part4"><strong>Part 4: Embed signing experience, redirects, and more</strong></a>
    </div>
  </td>
</tr>
</table>

## What you will need {#part1}

In part 1, you'll learn how to get started with everything you need for parts 2–4. Let's begin with getting API credentials.

* [Adobe Sign Developer Account](https://acrobat.adobe.com/us/en/sign/developer-form.html)
* [Starter Code](https://github.com/benvanderberg/adobe-sign-api-tutorial)
* [VS Code (or editor of your choice)](https://code.visualstudio.com)
* Python 3.x 
  * Mac — Homebrew
  * Linux — Built-in Installer
  * Windows — Chocolatey
  * All — https://www.python.org/downloads/

## Part 2: Low/No Code — the power of web forms {#part2}

In part 2, you'll explore the low/no-code option when using webforms. It’s always a good idea to see if you can avoid writing code at first.

1. Access Adobe Sign with your developer account.
1. Click **Publish a web form** on the home page.

   ![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_1.png)

1. Create your agreement.

   ![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_2.png)

1. Embed your agreement on a flat HTML page.
1. Experiment with dynamically adding query parameters.

   ![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_3.png)

## Part 3: Send agreement with a form and merge data {#part3}

In part 3, you'll dynamically create agreements.

First, you'll need to establish access. With Adobe Sign, there are two ways to connect via API. OAuth Tokens & Integration Keys. Unless you have a very specific reason to use OAuth with your application, you will want to explore Integration Keys first.

1. Select **API Information** under the **Account** tab in Adobe Sign.

   ![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_4.png)

Now that you have access and can interact with the API, see what you can do with the API.

1. Navigate to http://adobesign.com/public/docs/restapi/v6.

   ![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_5.png)

1. Use the token as a “bearer” value.

   ![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_6.png)

To send your first agreement it's best to understand how to use the API. 

1. Create a Transient Doc and send it. 

  >[!NOTE]
  >
  >JSON-based request calls have a “Model” and “Minimal Model Schema” option. This gives specs and a minimum payload set. 

  ![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_7.png)

After sending an agreement for the first time, you’re ready to add the logic. It’s always a good idea to establish some helpers to minimize repetition. Here are some examples:

**Validation**

![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_8.png)

**Headers/Auth**
  
![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_9.png)

**Base URI**

![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_10.png)

Be aware of where Transient docs land within the grand scheme of the Sign ecosystem.
Transient -> Agreement
Transient -> Template -> Agreement
Transient -> Widget -> Agreement

This example uses a template as our document source. This is usually the best route, unless you have a solid reason to dynamically generate documents for signature (e.g., legacy code or document generation).

The code is fairly straightforward; it uses a library document (template) for the document source. The first and second signers are dynamically assigned. The 'IN_PROCESS' state means that the document is being sent immediately. Also, 'mergeFieldInfo' is leveraged to dynamically fill fields.

![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_11.png)

## Part 4: Embed signing experience, redirects, and more {#part4}

In many scenarios, you may want to allow the triggering participant to immediately sign an agreement. This is useful for customer-facing applications and kiosks.

In this scenario, you probably don't want the first sending email to trigger. An easy way is to manage the behavior is with a modification to the API call.

![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_12.png)

Here's how to control the post-signing redirect:

![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_13.png)

After updating the agreement creation process, the final step is generating the signing URL. This call is also pretty straightforward and generates a URL that a signer may use to access their part of the signing process.

![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_14.png)

>[!NOTE]
>
>Note that the agreement creation call is technically asynchronous. This means a 'POST' agreement call can be made, but the agreement isn’t ready yet. The best practice is to establish a retry loop. Use a retry or whatever is the best practice for your environment.

![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_15.png)

When everything is put together, the solution is pretty straightforward. You’re making an agreement and then generating a signing URL for the signer to click on and begin the signing ritual.

**Additional topics:**

* [JS Events](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/events.md)
* Webhook Events
  * [REST API](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/webhooks/createWebhook)
  * [Webhooks in Adobe Sign v6](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/webhooks.md)
* [Reactivate Request Emails (with events)](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/updateAgreement)
* [Replace Timeout with a Retry](https://stackoverflow.com/questions/23267409/how-to-implement-retry-mechanism-into-python-requests-library)
* Custom Reminders
  * With the initial creation

  ![Screenshot of navigating to Power Automate](assets/embeddedesignature/embed_16.png)

  * Or add one [in-flight](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/createReminderOnParticipant)

### Additional Resources

http://bit.ly/Summit21-T126

Includes:
* Adobe Sign Developer Account
* Adobe Sign API Docs
* Sample Code
* Visual Studio Code
* Python














 










    
















 


















