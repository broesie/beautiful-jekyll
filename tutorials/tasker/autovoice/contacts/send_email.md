---
layout: tutorial
title: Send an e-mail to your contacts by using AutoVoice
---
This tutorial will explain, how to to send an e-mail to a specific contact.
We can use a command like this: **Send an e-mail to John.**

### Requirements:
- An android phone
- Tasker
- AutoVoice
- AutoContacts

### Step 1: AutoVoice & AutoContacts
Be sure that AutoVoice and AutoContacts are correctly installed. Also be sure, that all your contacts are listed in the database.
Before you start, refresh your contacts:
- **Open AutoContacts**
- Click on **Force Refresh Contacts**

### Step 2: Creating the profile
First, let's make a new profile, called **AV Contacts - Send Email**
- Create a new trigger/context: **Event > Plugin > AutoVoice > Recognized**
- Choose the **The Hard Way**
- Command: ```mail to (?<name>.+)```
- **Enable Regex**

### Step 3: Creating the task
Now we make our task, called **AV Contacts - Send Email**
- Flash: **Searching for names...**
- **AutoContacts Query 2.0**
  - Names: **%name**
  - Sort Direction: **Ascending**
  - Fields to get: **Email Address,Name,Id**
  - **Joiner=:=**
- **If %acname is Set**
  - Say: **The following contact has been found: %acname(1)**
  - **If %acemail is Set**
    - Flash: **%acemail**  
    - Say: **What would you like to include in your message?**
    - AutoVoice Recognize:
      - **Voice command without headset**
    - Compose Email: Recipient: **%acemail** if **%avcomm !~ cancel**
    - Say: **Ok, I will cancel your email** if **%avcomm ~R cancel**
  - **Else**
    - Say: **Sorry, this person doesn't have an emailaddress**
  - **Endif**
- **Else**
  - Say: **There is no contact found with that name**
- **End if**
