---
layout: tutorial
title: Control Home-Assistant by voice (in any language)
comments: true
---
This is a tutorial how you can control your devices by using your voice in your own language....
All this can be also triggered by Google Now.

## Requirements:
- An android phone
- Tasker
- AutoVoice

## Setup Tasker:

### Step 1: Create your configuration task

First I like to setup several thing, so I made a task, that I only need to run once... I'm putting my host, password and my devices in here. (When a device changes, then I only need to change it on 1 place, and all the other tasks will change as well).

#### So a config task would be like this in tasker:

- Variable set: **%HASS_PSW** to **?api_password=xxxxx**
- Variable set: **%HASS_SERVICE** to **http://xxxx:8123/api/services/** 
- Variable set: **%HASS_STATE** to **http://xxxx:8123/api/states/**

#### Add then your devices with your correct ID of HASS below eg:

- Variable set: **%HASS_WOL** to **switch.wol**
- Variable set: **%HASS_TOPLIGHT** to **light.living_toplight**
- Variable set: **%HASS_SIDELIGHT** to **light.living_sidelight**

After creating this, you need to run this task, so Tasker knows all the variables and remember it.

### Step 2: Configure your autovoice plugin:

- Open de app: **AutoVoice**
- **Activate Google Now integration**, if you want integration with Google Now
- Set your language: **General settings > Default Recognize Settings > Language Settings > Language (Also Language Code)**

Don't forget to enable in your android settings, the accessibility for Autovoice

### Step 3: Create your profile and task

#### Example 1: task to turn off/turn on task with if-else statements inside the task

##### Your profile:

- Create a new profile
- Choose **Event > Plugin > Autovoice Recognize**
- Choose **Advanced**
- **Checkmark Regex**
- As command filter use: ```(?<task>.+) my (?<device>.+)```

##### Your task:

Work with if-else function

I prefer to use just the If statement instead of the if-else statement, because I can collapse my code...
This is a task to turn on the living lights
- **If %task ~ turn on AND %device ~ living lights (turn on living lights)**
- Variable set: **%service to light/turn_on**
- **HTTP Post:**
 - Service port: **%HASS_SERVICE%service%HASS_PSW**
 - In data / file: **{"entity_id":"%HASS_TOPLIGHT","brightness":"255"}**
 - content/type: **application/JSON**
- **End if**

This is a task to turn off the living lights
- **If %task ~ turn off AND %device ~ living lights (turn off living lights)**
- Variable set: **%service to light/turn_off**
- **HTTP Post:**
 - Service port: **%HASS_SERVICE%service%HASS_PSW**
 - In data / file: **{"entity_id":"%HASS_TOPLIGHT"}**
 - content/type: **application/JSON**
- **End if**

...

#### Example 2: Dim lights task

##### Your profile:

- Create a new profile
- Choose **Event > Plugin > Autovoice Recognize**
- Choose **Advanced**
- **Checkmark Regex**
- As command filter use: ```dim (?<device>.+) to (?<percentage>.+)%```

##### Your task:

- **If %device ~ living lights**
- Variable set: **%service to light/turn_on**
- **HTTP Post:**
 - Service port: **%HASS_SERVICE%service%HASS_PSW**
 - In data / file: **{"entity_id":"%HASS_TOPLIGHT","brightness":"%percentage"}**
 - content/type: **application/JSON**
- **End if**

#### Other Commands

Above a little example to turn on or turn off things, but you can create also other profiles likes:

- ```dim (?<device>.+) to (?<percentage>.+)%```
- ```activate (?<scene>.+) mode```
- ....

You only need to change data and attributes...

The beauty of this, is that I can use Google now, so I can use Google AI to recognize my speech, and when I say a command by saying OK Google, it will also send it to my tasker autovoice...
