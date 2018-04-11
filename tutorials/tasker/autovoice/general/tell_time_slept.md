# Tell Time Slept
This task will tell you the time that you slept.

### Requirements:
- An android phone
- Tasker
- Autonotification

### Step 1: Register Startsleep
This action you trigger when you go to sleep. Eg: you can add this in your Night task.
- Variable set: **%Startsleep** to **%TIMES**

### Step 2: Creating the task (Stop Sleep)
Now we make our task, called **AV Time Slept**
- Variable set: **%Stopsleep** to **%TIMES**
- Variable set: **%timesleep** to **(%Stopsleep - %Startsleep)/3600** **(Enable: Do Math!)**
- Variable split: Name:**%timesleep** Splitter:**.** (Splitter: point)
- Variable set: **%hoursleep** to **%timesleep1**
- Variable set: **%timesleep2** to **0.%timesleep2**
- Variable set: **%minutesleep** to ```round(%timesleep2 * 60)``` **(Enable: Do Math!)**
- Flash: **You have slept for %hoursleep and %minutesleep minutes**
- Say: **You have slept for %hoursleep and %minutesleep minutes**
- **Autonotification**
  - Use HTML: **false**
  - Title: **Time slept**
  - Text: **You have slept for %hoursleep and %minutesleep minutes**
  - Icon: **Choose your icon**
  - Statusbar icon: **Choose your icon**
  
