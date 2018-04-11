# Notify when battery reach specific percentage
This tutorial will create a notificiation that will let you know when the battery reached a specific percentage.
This is pretty simple!

### Requirements:
- An android phone
- Tasker

### Example 1: Battery is full (100%)
#### Creating the profile
First, let's make a new profile, called **Battery 99-100**
- Create a new trigger/context: **State > Power > Battery Level**
- From **99** To **100**

#### Creating the task
Now we make our task, called **Battery 100%**
- Say: **The Battery is fully charged!**

As you see, it is pretty easy. You can create any notification on any percentage you want... So let's create another on 10%...


### Example 2: Battery is 10%
#### Creating the profile
First, let's make a new profile, called **Battery 09-10**
- Create a new trigger/context: **State > Power > Battery Level**
- From **9** To **10**

#### Creating the task
Now we make our task, called **Battery 10%**
- Say: **Attention, the battery percentage is now 10 percent. It's time to recharge!**

