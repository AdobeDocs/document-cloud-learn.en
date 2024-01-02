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
---
# Gather high-volume documents using GigaSign

Gigasign allows you to send, collect, and track documents for signature to thousands of people at the same time. It is designed for high-volume communications with your employees and customers--supporting up to 2,500 recipients with each bulk send. GigaSign uses the Acrobat Sign API to provide the same functionality as MegaSign, and includes support for multiple signers, recipient groups, recipient roles, agreement names, carbon copy, and more. 

>[!VIDEO](https://video.tv.adobe.com/v/328113?quality=12&learn=on&hidetitle=true)

## Download and install the GigaSign app

[Download GigaSign Zip File](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:d1a3f4f2-0f7b-466f-9785-81dff2217776)

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
