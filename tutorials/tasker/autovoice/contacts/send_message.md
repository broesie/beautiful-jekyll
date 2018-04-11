---
layout: tutorial
title: Send a message to your contacts by using AutoVoice
---
This tutorial will explain, how to to send a message to a specific contact.
We can use a command like this: **Send a message to John.**

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
First, let's make a new profile, called **AV Contacts - Send Message**
- Create a new trigger/context: **Event > Plugin > AutoVoice > Recognized**
- Choose the **The Hard Way**
- Command: ```send a message to (?<name>.+)```
- **Enable Regex**

### Step 3: Creating the task
Now we make our task, called **AV Contacts - Send Message**
- Flash: **Searching for names...**
- **AutoContacts Query 2.0**
  - Names: **%name**
  - Sort Direction: **Ascending**
  - Fields to get: **Name,Id,Phone Number**
  - **Joiner=:=**
- **If %acname is Set**
  - Variable set: **%number** to **%acnumber**
  - Flash: **The following contact has been found: %acname(1), what would you like to include in your message?**
  - Say: **The following contact has been found: %acname(1), what would you like to include in your message?**
  - AutoVoice Recognize:
    - **Voice command without headset**
  - Variable set: **%message** to **%avcomm**
  - Say: **The message is: %message and it is ready to send to %acname. Are you sure?**  
  - AutoVoice Recognize:
    - **Voice command without headset**
  - Send SMS: Number: **%acnumber** Message: **%message** if **%avcomm ~R yes**
- **Else**
  - Say: **There is no contact found with that name**
- **End if**
