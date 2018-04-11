# Call your contacts by using AutoVoice
This tutorial will explain, how to to call a specific contact.
We can use a command like this: **Call John.**

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
First, let's make a new profile, called **AV Contacts - Call**
- Create a new trigger/context: **Event > Plugin > AutoVoice > Recognized**
- Choose the **The Hard Way**
- Command: ```call (?<name>.+)```
- **Enable Regex**

### Step 3: Creating the task
Now we make our task, called **AV Contacts - Call**
- **AutoContacts Query 2.0**
  - Names: **%name**
  - Sort Direction: **Ascending**
  - Fields to get: **Phone Number,Name,Id**
  - **Joiner=:=**
- **If %acname is Set**
  - Flash: **The contact %acname(1) has been found**
  - Say: **The contact %acname(1) has been found**
  - Say: **Are you sure to call %acname(1)**
  - AutoVoice Recognize:
    - **Voice command without headset**
  - Call: **%acnumber** if **%avcomm ~R yes**
- **Else**
  - Say: **There is no contact found with that name**
- **End if**

