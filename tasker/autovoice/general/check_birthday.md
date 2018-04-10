# Check Birthdays
This task will check if there is a birthday today. If so, it will notify you.

### Requirements:
- An android phone
- Tasker
- AutoVoice
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

  
      
      
      
  - **If %acevent_next_date is Set**
    - Variable set: **%born_date** to **%acevent_start_date(1)**
    - Variable split: **%born_date** Splitter:**-**
    - Variable set: **%born_year** to **%born_date1**
    - Variable set: **%born_month** to **%born_date2 / 1** **(Do Math: Enabled!)**
    - Variable set: **%born_day** to **%born_date3**
    - AutoTools Time: Time span between dates
      - Start Date: **Year: %born_year**
      - Start Date: **Month: %born_month**
      - Start Day: **Day: %born_day**
      - End Date: **Use now: true**
    - Variable set: **%age** to **%atdateyears**
    - Variable set: **%monthindex** to **%born_month / 1** **(Do Math: Enabled!)**
    - Variable set: **%months** to **January,February,March,April,May,June,July,August,September,October,November,December**
    - Variable split: **%months** Splitter:**,** (Splitter is comma)
    - Say: **The birthday of %acname is on %born_day % months(%monthindex). This person is now %age years old**
  - **Else**
    - Say: **Sorry, no birthday has been found**
  - **End if**
- **Else**  
  - Say: **There is no contact found with that name**
- **End If**
