---
layout: post
title: Making test script creation, test and bug reports easier
description: 
headline: 
modified: 2017-08-09
category: Manual Testing
tags: [test scripts, exploratory testing, manual testing, bug report, test report, recording test results]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

### Making test script creation a breeze.

Over the past few months part of my role as a tester has been to create test scripts for exisiting customer journeys at the company I work for. As well as creating these test scripts I also have to record results of the test runs of these scripts as well as be able to report bugs reproducing the steps and any screenshots to help the team to resolve the issues I find.

Over a weekend I quickly knocked together a C# Windows Forms application - StepsRecorder.

![_config.yml]({{ site.baseurl }}/images/steps recorder.png)

This application isn't a silver bullet but it can greatly assist you. It's a very rough and ready version but I welcome any feedback to improve the tool or if you find any bugs please let me know!

### Limitations
Currently StepsRecorder only works in IE, I plan to enable users to be able to use Chrome and Firefox. StepsRecorder is also only available for Windows machines at this time.

### How to use StepsRecorder
- Press Record to start recording test steps.
- Select a web browser tab (the actor)
- Left click within a web browser tab records an action step
- Right click within a web browser tab records an expected result
- Double left click takes a screenshot

### Configuring StepsRecorder
There are a few options within the .config file which will enable you to customise the way in why you record test scripts, test and bug reports.

### Pre-populate URLs
Startup Urls option enables you to pre-populate the StepsRecorder search bar with urls for quick access. To add more than one url seperate it with a ,

key="StartupUrls" value="http://yoururl.co.uk/, http://anotherurl.com/"
    
#### Set IE Version
Here you can set the value to a specific version of IE or leave blank if you would like StepsRecorder to use the latest version of IE installed on your machine.

key="IEVersion" value="IE8"

#### Record Element Position
There is a very experimental setting which will enable you to record element positions, currently this is very hit and miss and needs a bit of dev work to improve this feature. Simply toggle this option on and off by switching the value to true for on or false for off.

key="RecordElementPosition" value="false"

#### Set browser tab names
When recording steps within StepsRecorder the currently selected web browser tab name is used to help create the recorded test steps. Within the .config you can customise the web browser tab names to change the 'actors' for the scripts.

key="BrowserTab1" value="User"
key="BrowserTab2" value="Developer"


### Download StepsRecorder
If you would like to try StepsRecorder you can download the .zip file from my Google Drive. [Download StepsRecorder](https://drive.google.com/open?id=0BypmF8SEg6CQM0tpSGcwaTNrdmc)

### Videos
Below are some very short videos to help you quickly get up and running with StepsRecorder

[StepsRecorder basics](https://youtu.be/B6_3UIDVbT4)

[Configuring StepsRecorder](https://youtu.be/cfelQ0GEumk)

### I would love your feedback
Good or bad, please let me know what you think of this tool or if you find any bugs!