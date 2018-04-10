# Tell Time
This task will tell you the current time. This is an extended version

### Requirements:
- An android phone
- Tasker

### Step 1: Creating the task
Now we make our task, called **AV Time**
- Variable split: Name:**%TIME** Splitter:**.** (Splitter: point)
- Variable set: **%time1** to **%TIME1 / 1** **(Enable: Do Math!)
- Variable set: **%time1** to **%TIME2** **(Enable: Do Math!)

- Say: **Goodmorning Name, did you sleep well** (Change Name by your name)
- Perform Task: **AV Time**
- Perform Task: **AV Date**
- Perform Task: **AV Time Slept**
- Perform Task: **AV Birthday Reminder Check**
- Say: **I'm now checking the weather**
- Perform Task: **AV Weather Forecast**
- Perform Task: **AV Events Today**

In my case I set the **priority** to **10** in each **Perform task**.
