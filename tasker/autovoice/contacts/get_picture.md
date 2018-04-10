# Get picture of your contacts by using AutoVoice
This tutorial will explain, how to retrieve the picture of a specific contact.
We can use a command like this: **show me a picture of John.**

## Requirements:
- An android phone
- Tasker
- AutoVoice
- Autocontacts

### Step 1: Create a folder where the picture will be stored
Create a folder **AutoContacts** on your phone. Mostly the full path will be something like this: **storage/emulated/0/AutoContacts/**

### Step 2: AutoVoice & AutoContacts
Be sure that AutoVoice and AutoContacts are correctly installed. Also be sure, that all your contacts are listed in the database.
Before you start, refresh your contacts:
- **Open AutoContacts**
- Click on **Force Refresh Contacts**

### Step 3: Creating the profile
First, let's make a new profile, called **AV Contacts - Picture**
- Create a new trigger/context: **Event > Plugin > AutoVoice > Recognized**
- Choose the **The Hard Way**
- Command: ```picture of (?<name>.+)```
- **Enable Regex**

### Step 4: Creating the task
Now we make our task, called **AV Contacts - Picture**
- **AutoContacts Query 2.0**
  - Names: **%name**
  - Sort Direction: **Ascending**
  - Fields to get: **Photo,Name,Id**
  - **Joiner=:=**
- **If %acname is Set**
  - **Autocontacts Details**
    - Contact Id: **%acid(1)**
    - Get Picture: **True**
    - Full Size: **True**
  - Flash: **%acpicturefile**
  - Open File: **%acpicturefile**
- **Else if %acname!Set**
  - Say: **There is no contact found with that name**
- **End if**

