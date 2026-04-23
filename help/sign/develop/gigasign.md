---
title: Gather High-Volume Documents using GigaSign
description: Gigasign allows you to send, collect, and track documents for signature to thousands of people at the same time
feature: Workflow
role: Developer
level: Intermediate
jira: KT-6626
topic-revisit: Integrations
thumbnail: 328113.jpg
exl-id: a59eab61-fe61-45c6-8137-f074e1f2b3ed
TQID: https://experienceleague.adobe.com/62xUXPGJ-H5XyknrYgKSEErD-mW0zIZc-qxQJvzXgCM
product_v2:
  - id: b12c730b-5ddb-4a2d-ba42-da774988b909
    internal-label: Acrobat
  - id: c1c5fb98-9105-44ed-9df1-9e04d062a784
    internal-label: Document Cloud
  - id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1
    internal-label: Adobe Sign
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
  - id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
    internal-label: Pass
feature_v2:
  - id: a1028f9a-6dbc-4a4f-adf5-eb9f85a408a6
    internal-label: Integrations
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
---
# Gather high-volume documents using GigaSign

Gigasign allows you to send, collect, and track documents for signature to thousands of people at the same time. It is designed for high-volume communications with your employees and customers--supporting up to 2,500 recipients with each bulk send. GigaSign uses the Acrobat Sign API to provide the same functionality as MegaSign, and includes support for multiple signers, recipient groups, recipient roles, agreement names, carbon copy, and more. 

>[!IMPORTANT]
>
>GigaSign is no longer being updated to the latest version of Java or Acrobat Sign and will only have limited support. The features of GigaSign are being added to the product under the [Send in Bulk](https://experienceleague.adobe.com/docs/document-cloud-learn/sign-learning-hub/admin-set-up/getting-started-admin/megasign.html?) functionality. Please use Send in Bulk for all usescases that do not explicitly require the use of GigaSign.

>[!VIDEO](https://video.tv.adobe.com/v/328113?quality=12&learn=on&hidetitle=true)

## Download and install the GigaSign app

[Download GigaSign Zip File](https://acrobat.adobe.com/id/urn:aaid:sc:US:001cf62d-1cab-46c7-aa96-661ac8680206)

[Java 1.8 download link (only if needed)](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) {target="_blank"}

[IP Addresses to white list (only if needed)](https://helpx.adobe.com/sign/system-requirements.html#IPs){target="_blank"}

## Basic setup instructions

1. Log in to your Acrobat Sign account.

1. Click **[!UICONTROL Group]** or **[!UICONTROL Account]**, whichever you see at the top.

1. Type "Access tokens" in the search field on the left side of the screen.

1. Press the "+" icon on the right side.

1. Create a key with the scopes needed (User_Read, Agreement_Read, Agreement_Write, Agreement_Send, Library_Read).

1. Double click the key you created and copy the FULL text (it goes off screen to the right so make sure you get it all).

1. Open GigaSign.

1. Click the **[!UICONTROL Settings]** icon at the top right.

1. Paste the integration key in the first line.

1. Enter the email address of the account used to create that key in the second line.

1. Click **[!UICONTROL Submit]**.
