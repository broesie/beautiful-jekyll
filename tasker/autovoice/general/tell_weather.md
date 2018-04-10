# Tell Weather Forecast
This task will tell you the weather forecast.

### Requirements:
- An android phone
- Tasker

### Step 1: Creating the task
Now we make our task, called **AV Time**
- Variable split: Name:**%TIME** Splitter:**.** (Splitter: point)
- Variable set: **%time1** to **%TIME1 / 1** **(Enable: Do Math!)**
- Variable set: **%time1** to **%TIME2**
- **If %time1>12**
  - Variable set: **%time1** to **%time1 - 12** **(Enable: Do Math!)**
- **Else**
  - Variable set: **%time1** to **%time1**
- **End if**
- **If %time2 = 15**
  - Variable set: **%time2** to **quarter past**
  - Say: **It is now %time2 %time1**
- **Else if %time2 = 30**
  - Variable set: **%time2** to **half past**
  - Say: **It is now %time2 %time1**
- **Else if %time2 = 45**
  - Variable set: **%time2** to **quarter to**
  - Variable set: **%time1** to **%time1 +1** **(Enable: Do Math!)**
  - Say: **It is now %time2 %time1**
- **Else if %time2 = 00**  
  - Say: **It is now %time1 o'clock**
- **Else**
  - Say: **It is now %time1 hour %time2**
- **End if**
  
### Step 2: Creating the profile
If you want to use it with your voice assistant, you can also create a profile. Create a AutoVoice context/trigger.
Call the profile: **AV Time**
- Create a new trigger/context: **Event > Plugin > AutoVoice > Recognized**
- Choose the **The Hard Way**
- Command: ```what time is it```
- **Enable Regex**
- Link the task **AV Time** to it
