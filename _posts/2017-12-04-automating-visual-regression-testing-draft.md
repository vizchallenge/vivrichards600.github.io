---
layout: post
title: Automating visual regression testing
description: 
headline: 
modified: 2017-05-27
category: Automation
tags: [Automation, Visual testing, Regression testing, UAT, Manual testing]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

### Why automate tests in the first place?

There are many advantages to test automation. Most are releated to the repeatability of the tests and the speed at which tests can be executed.

Automated testing can be more reliable as it is performed by tools and/or scripts. Automated testing is executed by software tools, so it offers a significantly fast approach than manually testing. It can help save you both time and money running checks which normally you would have to repeat manually, over and over again.

### Common automation issues

When looking to invest implement automated testing there are many hurdles which can stop you dead in your tracks. One of the most common issues is the investment required for testing tools. Often tools costs money, but even when they are free (open source), there is usually a lot of time which needs to be invested in order to correctly implement the automated checks, ensuring the team are comfortable in using the new tools and that they are achieving what was intended. One of the biggest issues I have found when using automated tests is that **automated testing does not entail human observation** and cannnot guarantee user-friendliness or positive customer experience.

> "It can be a slippery slope"

Quite often when people are shown new tools or frameworks it's very easy to get carried away. When looking to automate tests it is important to automate what rights, just because you can it doesn't mean you should!

### Ice-cream cone anti pattern

The Ice-Cream Cone anti-patte

> "But I don't have enough time .."

**Manually repeating tests is costly and time consuming!** Automating software testing can reduce the time to run repetitive tests from days to hours.

It's suprising how often you hear people talk about how they do not have time to automate or that they think test automation is a duplication of effort. 

Of course you shouldn't automate everything, but if you can automate just a few tests this could not only save you time but also give you confidence in the software in which you are releasing. Once created automated tests can be run over and over again at no additional cost - and they are much faster to run than manually testing over and over again.

### Automation advantages

Test automation has specific advantages for improving the long-term efficieny of a software team's testing processes.

Test automation supports:
* Frequent regression testing
* Rapid feedback to developers
* Virtually unlimited iterations of test case execution
* Support for Agile and extreme development methodologies
* Disciplined documentation of test cases
* Customized defect reporting
* Finding defects missed by manual testing

### Testing pyramid

Below is an example of the testing pyramid. The higher the level, the slower and more brittle testing becomes. As well as all of the automation effort a large part of testing is still done manually, adding to the time and cost to deliver quality software.

In this blog post we're going to focus on the top end of the triangle, looking at ways to improve implementation and execution time as well as adding extra value to our tests.

![_config.yml]({{ site.baseurl }}/images/pyramid.png)

_The above image is an adaption from http://martinfowler.com/bliki/TestPyramid.html_

### How valuable are these tests?

Below is some C# code which is using Selenium WebDriver. This is a basic type of UI automated test I've written to demonstrate an automated test you'd typically see people write. Here I am Asserting elements are rendered on a contact form displaying their expected text.
 
![_config.yml]({{ site.baseurl }}/images/form1.png)

### Humans Vs Machines

Before we go to much further, how good do you think you are at finding differences? Below there are a number of differences between the two images. Once you think you've found them all continue reading.

![_config.yml]({{ site.baseurl }}/images/spotdiff.png)

### How many differences did you find?

There were **5** differences, did you find them all? Sometimes it's difficult to know where all the differences are and to know when to stop checking, having the confidence to know we've found all the differences.

![_config.yml]({{ site.baseurl }}/images/spotdiffdiffs.png)

### Remember this code?

This was a basic Selenium WebDriver automation test I'd created in C# to Assert that elements were rendered on a contact form along with the text I expected.
 
![_config.yml]({{ site.baseurl }}/images/form1.png)

### There's been a change

The image below shows some changes somebody has made to the contact form. They decided to make a change or refactor some code and pushed their code which has changed the contact form. 

How many of the below tests would now fail because of this change?

![_config.yml]({{ site.baseurl }}/images/form2.png)

### Only two Asserts would fail!

A developer noticed the two failing tests and makes the required code changes to fix the two failing tests. The tests are now re-run and all the tests now pass and so the developer now moves on to doing something else. Unfortunately the layout of the form is now messed up - hopefully these changes are picked up when manually testing the site before the changes are rolled out!

![_config.yml]({{ site.baseurl }}/images/formasserts.png)

### Saving time and cost

What if we could not only automate the UI but some tests typically carried out by manual or exploratory testing? These type of tests could save us lots of time and money whilst also giving us the confidence that unexpected differences like the ones in the UI above could be found.

![_config.yml]({{ site.baseurl }}/images/pyramid2.png)


### Could it be this simple?

What if we could automate some visual testing which could pick up visual changes to our software? No longer just checking elements and text have been rendered on our web applications with typical UI automated tests, but comparing what our page looks like and what we expect it to look like.

![_config.yml]({{ site.baseurl }}/images/form3.png)

### Easier to maintain tests

What if we could replace many of the Selenium Tests which simply asserted whether fields, and text were displayed to the end user, using just one or two lines of code instead of many to implement.  

The cost to maintain these tests are kept to a minimum, we no longer have to worry about element Id’s/classes changing, updating tests for correct wording etc.

![_config.yml]({{ site.baseurl }}/images/oldnewcode.png)

### Catch more bugs!

With these additional tests we can gain an extra depth to our tests and assert things which would generally be left down manual testing. Now we have the ability to possibly catch even more bugs to do with layouts, colours and text before we release our software into the wild!

![_config.yml]({{ site.baseurl }}/images/form1.png)

### Quicker execution

It all depends on the type of tests your writing but these tests often take a lot less lines of code to write and also execute quicker. No longer asserting each element exists and it’s text is what you expect – just one Assert is all it takes.

This additional **visual** automation testing can reduce test execution time dramatically

![_config.yml]({{ site.baseurl }}/images/execution.png)

### How accurate is automated visual testing?

Visual regression tests accuracy depends on the framework/tool you use but with most it can detect a single letter difference. 

### Yeah but could it find Wally?

To test just how quick and accurate visual testing could be I took a Where’s Wally image and then made a copy of this image and removed Wally and put it to the test!

![_config.yml]({{ site.baseurl }}/images/wallys.png)

### Let's zoom in just for us humans!

I’ve zoomed in here just to make it a bit easier for us to try and find Wally. It’s still fairly difficult to find him even with more than 50% less of the image removed for us to try and spot the difference!

![_config.yml]({{ site.baseurl }}/images/zoom.png)

### Got him!

![_config.yml]({{ site.baseurl }}/images/zoomanswers.png)

Let’s see how well the visual test did..

**No problem!**

By providing two images with a tiny difference, the automated visual test took just 293 ms to find Wally and notify us of a failure!

We also have some flexibility in these test, we have the ability to compare images which hopefully have the same content but may be different sizes or different file types. We can also decide on what we deem to be an acceptable percentage to allow the images to differ.

![_config.yml]({{ site.baseurl }}/images/vsexecute.png)

### Another tool to add to your belt

You still need automated functional and end to end tests - visual testing cannot replace this.

Visual regressions testing isn’t trying to replace these types of tests, but where possible provide extra quality assurance in the software we deliver - having the ability to see and assert what the user sees and to assert the sotware UI meets our expectations.

At it’s most basic, Visual regression testing is a series of tests that can run through your site, taking screenshots and comparing those screenshots against a baseline, alerting you when things change.

### Try it for yourself

There are many tools and frameworks out there for doing visual regression testing but unfortunately they didn't quite match my requirements and so I put together something myself which utilises C# and Selenium WebDriver.

If you'd like to try some automated visual testing yourself [the code can be found by visiting my GitHub page](https://github.com/vivrichards600/AutomatedVisualTesting). 

The framework is very light weight and currently enables you to to compare differences between; two images, an image and a website url or an image and a pdf page. The framework is very accurate and can detect a single pixel difference using any of the methods above. When differences are found, a copy of the original image is taken and areas where differences were found are drawn on the image and saved locally to help you see what went wrong. [Checkout the project over on GitHub](https://github.com/vivrichards600/AutomatedVisualTesting) for further info and to try it yourself!

![alt text](https://github.com/vivrichards600/AutomatedVisualTesting/blob/master/AutomatedVisualTesting/TestData/diff.png?raw=true "Chrome Differences Screenshot")

### Slides

I've given this talk this month at a [local meet-up](https://www.meetup.com/Swansea-Software-Development-Meetup) and it had a great reception. If you are interested, the slides can be found here: [Automating Visual Regression Testing](https://www.slideshare.net/vivrichards/spot-the-difference-automating-visual-regression-testing) *

* This talk has since been given at DDD East Anglia and DDD North and so the slides have been updated.
