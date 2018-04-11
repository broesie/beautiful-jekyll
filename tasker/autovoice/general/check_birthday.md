---
layout: tutorial
title: First post!
---

# Check Birthdays
This task will check if there is a birthday today. If so, it will notify you.

### Requirements:
- An android phone
- Tasker
- AutoNotification
- AutoContacts
- AutoTools

### Step 1: AutoContacts
Be sure that AutoContacts is correctly installed. Also be sure, that all your contacts are listed in the database.
Before you start, refresh your contacts:
- **Open AutoContacts**
- Click on **Force Refresh Contacts**

### Step 2: Creating the task
Now we make our task, called **AV Birthday Reminder Check**
- **AutoContacts Query 2.0**
  - Sort: **event_next_date**
  - Fields to get: **Id,Event Next Date,Name,Event Start Date,Event Type Label**
  - **Joiner=:=**
- **For** Variable: **%index** Items: **1:%acevent_next_date(#)**
    - AutoTools Time: 
      - End Date: **Use now: true**
      - Fields to get: **Total hours**
    - **If %atdatetotalhours>0**
      - Variable set: **%Bdayname** to **%acname(%index)**
      - Variable set: **%contactid** to **%acid(%index)**
      - Variable set: **%event** to **%acevent_type_label(%index)**
      - Variable set: **%borndate** to **%acevent_start_date**
      - Variable split: **%borndate** Splitter:**-**
      - Variable set: **%monthindex** to **%borndate2 / 1** **(Do Math: Enabled!)**
      - Variable set: **%months** to **January,February,March,April,May,June,July,August,September,October,November,December**
      - Variable split: **%months** Splitter:**,** (Splitter is comma)
      - AutoTools Time:
        - Start Date: Year: **%borndate1**
        - End Date: **Use now: true**
      - Variable set: **%Bdayyears** to **%atdateyears**
      - **AutoContacts Query 2.0**
        - Ids: **contactid**
        - Phone Type: **Mobile**
        - Sort Direction: **Ascending**
        - Fields to get: **Phone Number,Id,Phone Number Type,Name**
        - Joiner: **=:=**
      - **AutoContacts Details**
        - Contact Id: **%acid**
        - Get Picture: **true**
        - Full Size: **true**
      - **If %acnumber is Set**
        - Variable set: **%Bdaynr** to **%acnumber**
        - **AutoNotification**
          - Title: **%event today**
          - Text: **It's %name's birthday. He/She was born on %borndate3 %months(%monthindex) %borndate1. He/She becomes %atdateyears years old.**
          - Icon: **/storage/emulated/0/AutoContacts/contactPhoto.png**
          - Statusbar Icon: **ic_action_balloon**
          - Statusbar Text Size: **16**
          - Id: **Next event**
          - Button 1: **smsbday**
          - Label 1: **MESSAGE**
          - Icon 1: **ic_action_sms**
          - Button 2: **callbday**
          - Label 2: **CALL**
          - Icon 2: **ic_action_phone_start**
      - **Else if %acnumber !Set**
        - **AutoNotification**
          - Title: **%event today**
          - Text: **It's %name's birthday. He/She was born on %borndate3 %months(%monthindex) %borndate1. He/She becomes %atdateyears years old.**
          - Icon: **/storage/emulated/0/AutoContacts/contactPhoto.png**
          - Statusbar Icon: **ic_action_balloon**
          - Statusbar Text Size: **16**
          - Id: **Next event**
          - Icon 1: **ic_action_sms**
          - Icon 2: **ic_action_phone_start**
      - **End if**
  - **Else**
    - **Stop**
  - **End if**
- **End for**

### Step 3: Creating a task that react on the call button
Create a task, called **AN B-day Call**
- Call Number: **%Bdaynr**

### Step 4: Creating a task that react on the message button
Create a task, called **AN B-day SMS**
- Autonotification Cancel: Configuration: **Id:Next event**
- Status Bar **Collapsed**
- **If %Bdaynr is Set**
  - Variable set: **%bdaytext** to **Happy B-day and many years! Enjoy! Greetings Ryoen**
  - **AutoTools Web Screen** (I created my own webscreen, so I can change my text if I want and personalize it more before I send it. This webscreen is not included here)
- **Else if %Bdaynr !Set**
  - Flash: **Sorry, no mobile number is found**
- **End If**

### Step 5: Creating a profile to react on the call button
Call the profile: **AN B-day Call**
- Create a new trigger/context: **Event > Plugin > AutoNotification > AutoNotification**
- AutoNotification: **callbday**
- Link it to the task **AN B-day Call**

### Step 6: Creating a profile to react on the call button
Call the profile: **AN B-day SMS**
- Create a new trigger/context: **Event > Plugin > AutoNotification > AutoNotification**
- AutoNotification: **smsbday**
- Link it to the task **AN B-day SMS**
