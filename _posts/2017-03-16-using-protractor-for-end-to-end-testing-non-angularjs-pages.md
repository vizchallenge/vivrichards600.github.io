---
layout: post
title: Browser automation using Protractor on non AngularJs pages
description: 
headline: 
modified: 2017-03-16
category: Automation
tags: [Automation, Selenium, WebDriver, JS, Protractor]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

![Protractor](http://www.perfomatix.com/wp-content/uploads/2016/03/workflow1-1.jpg) 

> Protractor is an end-to-end test framework for Angular and AngularJS applications. Protractor runs tests against your application running in a real browser, interacting with it as a user would.

Below we will go through how to setup a simple JavaScript test using Protractor and using an example QA Engineer assignment to test.

## Prerequisites

Protractor is a Node.js program. To run, you will need to have Node.js installed https://nodejs.org/en/. You will download Protractor package using npm, which comes with Node.js. Check the version of Node.js you have by running `node --version`. Then, check the compatibility notes in the Protractor README to make sure your version of Node.js is compatible with Protractor.


## Setup

Use npm to install Protractor globally with: `npm install -g protractor`

This will install two command line tools, protractor and webdriver-manager. Try running `protractor --version` to make sure it's working.

The webdriver-manager is a helper tool to easily get an instance of a Selenium Server running. Use it to download the necessary binaries with: `webdriver-manager update`

Now start up a server with: `webdriver-manager start`

This will start up a Selenium Server and will output a bunch of info logs. Your Protractor test will send requests to this server to control a local browser. You can see information about the status of the server at http://localhost:4444/wd/hub.


## Write a test
Open a new command line or terminal window and create a clean folder for testing.

Protractor needs two files to run, a spec file and a configuration file.

Let's create a simple test that navigates to the home page of the computers database site and attempts to read some of the text from the `h1` heading on the top of the page.

Copy the following into HomePageSpec.js:

`describe('Computers database homepage', function() {
  
  it('should be displayed', function() {
    browser.get('http://computer-database.herokuapp.com/computers');

    var pageHeading = element(by.id('main')).element(by.css('h1'));
    expect(homepage.heading.getText()).toContain(' computers found')
  });
  
  beforeEach(function() {
	// We aren't running Angular so do not want to wait for Angular promises!
		return browser.ignoreSynchronization = true;
	});
  
}); `

The describe and it syntax is from the Jasmine framework. browser is a global created by Protractor, which is used for browser-level commands such as navigation with browser.get. The beforeEach function is what we include to enable us to run Protractor Javascript tests against non AngularJs pages, this ensures our tests don't hang about waiting for Angular promises! Failure to have this in our test specs will cause tests to fail.

Configuration
Now create the configuration file. Copy the following into conf.js:

`exports.config = {
  seleniumAddress: 'http://localhost:4444/wd/hub',
  specs: ['HomePageSpec.js']
};`

This configuration tells Protractor where your test files (specs) are, and where to talk to your Selenium Server (seleniumAddress). It will use the defaults for all other configuration. Chrome is the default browser.

## Run the test
Now run the test with: `protractor conf.js`

You should see a Chrome browser window open up and navigate to computers database page, then close itself (this should be very fast!). The test output should be 1 test, 1 assertion, 0 failures. Congratulations, you've run your first non AngularJs Protractor Javascript test!

That's pretty much all there is to the basics in getting up and running.

 If you would like to see further examples and/or give the QA assignment a go, please view my [QA Assignment submission](https://github.com/vivrichards600/QATestingCaseKata) 
