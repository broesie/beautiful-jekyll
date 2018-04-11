---
layout: tutorial
title: Tell Date
---
This task will tell you the current date. This is the long format.

### Requirements:
- An android phone
- Tasker

### Step 1: Creating the task
Now we make our task, called **AV Date**
- Variable split: Name:**%DATE** Splitter:**-**
- Variable set: **%monthindex** to **%DATE1 / 1** **(Enable: Do Math!)**
- Variable set: **%months** to **January,February,March,April,May,June,July,August,September,October,November,December**
- Variable split: **%months** Splitter:**,** (Splitter is comma)
- Variable set: **%year** to **20%DATE3**
- Say: **It is now %DAYW %DATE2 %months(%monthindex) %year**
  
### Step 2: Creating the profile
If you want to use it with your voice assistant, you can also create a profile. Create a AutoVoice context/trigger.
Call the profile: **AV Date**
- Create a new trigger/context: **Event > Plugin > AutoVoice > Recognized**
- Choose the **The Hard Way**
- Command: ```what's the date```
- **Enable Regex**
- Link the task **AV Date** to it
