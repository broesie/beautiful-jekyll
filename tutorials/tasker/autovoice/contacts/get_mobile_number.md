---
layout: tutorial
title: Get the mobile phone number of your contacts by using AutoVoice
---
This tutorial will explain, how to retrieve the mobile phone number of a specific contact.
We can use a command like this: **What's mobile of John.**

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
First, let's make a new profile, called **AV Contacts - Mobile Number**
- Create a new trigger/context: **Event > Plugin > AutoVoice > Recognized**
- Choose the **The Hard Way**
- Command: ```mobile of (?<name>.+)```
- **Enable Regex**

### Step 4: Creating the task
Now we make our task, called **AV Contacts - Mobile Number**
- **AutoContacts Query 2.0**
  - Names: **%name**
  - Sort Direction: **Ascending**
  - Fields to get: **Phone Number,Id,Phone Number Type,Name**
  - **Joiner=:=**
- **If %acname is Set**
  - Variable Set: **%index** to **%acnumber_type(#?Mobile)**
  - Variable Split: **Name:%index** Splitter:**,** (splitter is a comma)
    - **If %index!~0**
      - Flash: **%acname %acnumber(%index1)**
      - Say: **The mobile phone number of %acname is %acnumber(%index1)**
    - **Else**
      - Say: **Sorry, %acname doesn't have any mobile phone number**
    - **End if**
- **Else**
  - Say: **There is no contact found with that name**
- **End if**
