---
layout: tutorial
title: Good morning task
---
This task is a combination of many other tasks. You can execute that every morning.
When this task is executed, it will do many things like: saying morning message, tell me the weather, tell me the birthdays today, tell me my appointments, etc...

### Requirements:
- An android phone
- Tasker

### Step 1: Creating the task
Now we make our task, called **AV Good Morning**
- Say: **Goodmorning Name, did you sleep well** (Change Name by your name)
- Perform Task: **AV Time**
- Perform Task: **AV Date**
- Perform Task: **AV Time Slept**
- Perform Task: **AV Birthday Reminder Check**
- Say: **I'm now checking the weather**
- Perform Task: **AV Weather Forecast**
- Perform Task: **AV Events Today**

In my case I set the **priority** to **10** in each **Perform task**.
