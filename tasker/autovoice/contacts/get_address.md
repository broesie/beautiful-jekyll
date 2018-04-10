# Get the address of your contacts by using AutoVoice
This tutorial will explain, how to retrieve the address of a specific contact.
We can use a command like this: **What's the address of John.**

## Requirements:
- An android phone
- Tasker
- AutoVoice
- Autocontacts

### Step 1: AutoVoice & AutoContacts
Be sure that AutoVoice and AutoContacts are correctly installed. Also be sure, that all your contacts are listed in the database.
Before you start, refresh your contacts:
- **Open AutoContacts**
- Click on **Force Refresh Contacts**

### Step 2: Creating the profile
First, let's make a new profile, called **AV Contacts - Address**
- Create a new trigger/context: **Event > Plugin > AutoVoice > Recognized**
- Choose the **The Hard Way**
- Command: ```address of (?<name>.+)```
- **Enable Regex**

### Step 4: Creating the task
Now we make our task, called **AV Contacts - Address**
- **AutoContacts Query 2.0**
  - Names: **%name**
  - Sort Direction: **Ascending**
  - Fields to get: **Address City,Address Street,Address,Address Postal Code,Id,Address Country,Name**
  - **Joiner=:=**
- **If %acname is Set**
  - **If %acaddress is Set**
    - Say: **The address of %acname is %acaddress.**
  - **Else if %acaddress!Set**
    - Say: **Sorry, I couldn't find any address of that contact**
  - **End if**
- **Else**
  - Say: **There is no contact found with that name**
- **End if**
