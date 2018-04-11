---
layout: tutorial
title: Get age of your contacts by using AutoVoice
---
This tutorial will explain, how to retrieve the age of a specific contact.
We can use a command like this: **how old is John.**

### Requirements:
- An android phone
- Tasker
- AutoVoice
- AutoContacts
- AutoTools

### Step 1: AutoVoice & AutoContacts
Be sure that AutoVoice and AutoContacts are correctly installed. Also be sure, that all your contacts are listed in the database.
Before you start, refresh your contacts:
- **Open AutoContacts**
- Click on **Force Refresh Contacts**

### Step 2: Creating the profile
First, let's make a new profile, called **AV Contacts - Age**
- Create a new trigger/context: **Event > Plugin > AutoVoice > Recognized**
- Choose the **The Hard Way**
- Command: ```how old is (?<name>.+)```
- **Enable Regex**

### Step 4: Creating the task
Now we make our task, called **AV Contacts - Age**
- **AutoContacts Query 2.0**
  - Names: **%name**
  - Sort Direction: **Ascending**
  - Fields to get: **Id,Event Start Date,Event Next Date,Name**
  - **Joiner=:=**
- **If %acname is Set**
  - Variable set: **%born_date** to **%acevent_start_date(1)**
  - Variable split: **%born_date** Splitter:**,** (splitter is comma)
  - Variable set: **%born_year** to **%born_date(1)**
  - Variable set: **%born_month** to **%born_date2 / 1** **(Do Math: Enabled!)**
  - Variable set: **%born_day** to **%born_date3**
  - AutoTools Time: Time span between dates
    - Start Date: **Year: %born_year**
    - Start Date: **Month: %born_month**
    - Start Day: **Day: %born_day**
    - End Date: **Use now: true**
  - Variable set: **%age** to **%atdateyears**
  - Say: **%acname is now %age years old**
- **End If**  
- **If %acname!Set**
  - Say: **There is no contact found with that name**
- **End if**

