---
layout: tutorial
title: Notify when battery is charging and decharging
---
This tutorial will create a notificiation that will let you know when the battery is charging or decharging. It can be useful eg when the cable doesn't give good contact, etc...

### Requirements:
- An android phone
- Tasker

### Step 1: Create a charging task
Call the task: **Battery - Recharge**
- Say: **The Battery is now charging!**

### Step 2: Create a decharging task
Call the task: **Battery - Decharge**
- Say: **Attention, The Battery is now decharging!**

### Step3: Creating the profile
First, let's make a new profile, called **Battery Charge**
- Create a new trigger/context: **State > Power > Power**
- Link the task **Battery - Recharge** to it
- Now longpress on your profile context, and choose **Exit Task**
- Choose **Battery - Decharge** as exit task
