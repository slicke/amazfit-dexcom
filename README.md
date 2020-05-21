# Get your BG readings on your Amazfit GTS (maybe more?)

## What's this?
I got an Amazfit GTS and thought that it would be nice to connect it to my Dexcom. Keeping in mind the watch doesn't support Dexcom and the Amazfit integration in xDrip+ is so-so (and recent G6 transimitters are not working well), my expectations were not great. However, I managed to cook something up. I'm sharing this for others, and I will try to update it when I get more work done. It's not intended as a real project, just a reference. Feel free to improve on it!

Also note, some messages are in Swedish - just change them to your own)

## What does it do?
Basically it shows your BG value as a pop-up notification when you press the watch button twice in a row.

## How does it do it?
It reads the G6 notification on your mobile and extracts data from it.

### Does it do the graph?
No.

### Does it show trends?
Working on it.

### What will I get?
Your current reading and the time it was collected.

# What do I need?
## Amazfit Tools
You need an app called Amazfit Tools (it allows you to customize lots of things, including watchface, notifications from apps, interations with Sleep as Anroid, ...).
I tried some apps and I fell for this one as it integrates with _Tasker_ (see below), I'm not connected to the developer.

## Tasker
Tasker allows you to run scripts and automation on your phone. Amazfit Tools integrate with Tasker, to let you run tasks/scripts when the button is pressed,

### Tasker AutoNotification
This is an extension that lets Tasker read notifications

# Getting started
>### Warning!
> You should NOT do this unless you have a good understanding of computers and have used Tasked before, or have help from someone!
> The steps are quite complicated and you need to buy some apps, do NOT do this unless you are 100% certain you want to buy them and have other uses for them!
> This is a __reference__ to how one can do things, not an officiall app, guide and there are not guarantees!

Make sure you have [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm&hl=sv), [AutoNotification](https://play.google.com/store/apps/details?id=com.joaomgcd.autonotification) and [AmazFit Tools](ay.google.com/store/apps/details?id=cz.zdenekhorak.amazfittools) installed.

- Create new profile
-- Use _Event_ as type
-- Choose _Plugin_ as category
-- Choose the _Amazfit Tools_ plugin (restart Tasker if you don't see it)
- Select _Button Pressed_ as event trigger

You now have an event, which will fire when you click the watch button. In the task, we will set the number of presses to 2.

You can now import the task in tasker from my share link [here](https://taskernet.com/shares/?user=AS35m8lYCHsfXeEtUwtQcBIhgVf6FhsiyWUMypau7fFdz%2F4IVv6U%2BoR45HzTP9FpjdgNdQ%3D%3D&id=Task%3AL%C3%A4s+Dexcom)

Done!

# Details
The task as 6 steps:
- AutoNotification Query
-- Persistant notifications
-- App(s): Dexcom G6
-- Advanced: Get all fields
-- If-starement, to only trigger when "%button_count" EQ 2.
- Variable %dextid
-- Takes the %anwhentime variable, which uses milliseconds and divides it to seconds
- Variable conversion of %dextid to date time
- Variable section, cut out the time and dismiss the data
- Variable %dexval is set to the 1 and 2 word of the Dexcom text (being reading and unit, eg "5.5" and "mmol/L")
- Watch push
-- Amazfit Tools is called upon to create a _Custom Notification_ with the time and reading:
-- Title: %anapp() will translate to Dexcom G6 - you can choose eg "Blood sugar" or something here
-- Content includes %dextid as placeholder for time and %dexval for the reading

# All set
Have a nice day!
