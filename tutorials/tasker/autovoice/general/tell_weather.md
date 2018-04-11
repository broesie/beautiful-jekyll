# Tell Weather Forecast
This task will tell you the weather forecast using Wunderground.

### Requirements:
- An android phone
- Tasker
- AutoWeb

### Step 1: Creating the task
Now we make our task, called **AV Weather Forecast**
- AutoWeb
  - API: **Weather Underground**
  - API Action: **Conditions**
  - Query: **Country/City** eg: US/New York
  - Language: **Your language code**
- Flash: **%display_location_full %temp_c %weather** you can also use f for fahrenheit
- Say: **The weather forecast: Today: %weather, it is now %temp_c degrees celcius. The maximum temperature is %highcelcius(1) degrees celcius and the minimum temperature is %lowcelcius(1) degrees celcius. The probability of rain is %rainprobability(1) procent and the humidity is %relative_humidity.**
  
### Step 2: Creating the profile
If you want to use it with your voice assistant, you can also create a profile. Create a AutoVoice context/trigger.
Call the profile: **AV Weather Forecast**
- Create a new trigger/context: **Event > Plugin > AutoVoice > Recognized**
- Choose the **The Hard Way**
- Command: ```what's the weather```
- **Enable Regex**
- Link the task **AV Weather Forecast** to it
