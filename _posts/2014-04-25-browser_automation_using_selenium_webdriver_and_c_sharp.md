---
layout: post
title: Browser automation using Selenium WebDriver and C#
description: 
headline: 
modified: 2014-04-25
category: Automation
tags: [Automation, Selenium, WebDriver, C#]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

![SeleniumWebDriver](https://i0.wp.com/learn-automation.com/wp-content/uploads/2015/08/Cross-browser-testing-in-Selenium-Webdriver.png?fit=525%2C333)

### Initial Project Setup 
Create a new Unit Test Project within Visual Studio - for this example it is a C# project.

Next we will install Selenium WebDriver by using NuGet. Run the following command in the [Package Manager Console](https://docs.nuget.org/docs/start-here/using-the-package-manager-console):
`Install-Package Selenium.WebDriver`

[Download the C# Chrome Driver](https://chromedriver.storage.googleapis.com/index.html?path=2.29/) as we will need this as we will be testing within a Chrome browser.
Open the downloaded .zip file and Extract the chromedriver.exe in to your Visual Studio project folder.
Next right click chromedriver.exe within your project and click properties. We want to ensure every time the project is built chromedriver.exe is copied to the output directory so that we can ensure the Chrome driver exists to run our tests. Set 'Copy to Output Directory' property to 'Copy if newer'

Edit class, UnitTest1.cs and be sure to give it a meaningfull name.

Now open up the unit test you just renamed. We need to add some imports to the top of our test in order for us to be able open up a new web browser and do stuff. Add to the top of the test class the below two usings;

`
using OpenQA.Selenium.Chrome;
using OpenQA.Selenium;
`

### Setting up some test class attributes
Before and after running our tests we want to ensure we create a Chrome browser to run all of our tests and then ensure we quit any instances of the Chrome browser we've opened, we will do this by creating TestInitialize and TestCleanup test attributes. Here we can create a new Chrome web driver instance and then once all tests have finished we can quit the Chrome browser driver instance.

Paste the following into the new class

	public static IWebDriver WebBrowser;

	[TestInitialize()]
	public void Initialization()
	{
		WebBrowser = new ChromeDriver();
	}

	[TestCleanup()]
	public void Termination()
	{
		WebBrowser.Quit();
	}


So now in our code we have a method to create a new Chrome driver instance to run each of our tests and a method to close any instances of our Chrome browser which may be running to keep things tidy.

### Creating our first regression test to test the home page is presented

The web application we will be creating automated tests for will be the [Computers Database](http://computer-database.herokuapp.com/computers).
The first thing to do is to rename the TestMethod1() to something more meaningful, this is where we will put our first test. This test will be to check the computer home page is displayed.

`   [TestMethod]
	public void Home_Page_Should_Be_Presented()
	{
	  //TODO
	}
`

Next we will want to get our test to actually navigate to the website we are testing and check it is being displayed by reading the page title. Go to where our test says `//TODO` and replace this text with the below code - this will be where we tell the Chrome WebDriver to navigate to the page and then check the page title equals what we expect it to.

` WebBrowser.Navigate().GoToUrl("http://computer-database.herokuapp.com/computers");
	Assert.IsTrue(WebBrowser.Title.Equals("Computers database"));`

	
### Testing finding elements and navigating between pages

Using WebDriver we are able to find elements and interact in a number of different ways. Below we will create a test to find the 'Add a computer' button on the home page and click it to navigate to the 'Add a computer' page. Next we will then attempt to check the page heading on the 'Add a computer' page by locating the H1 element which is nested within an element with the Id of 'main'.

 
  [TestMethod]
public void Home_Page_Should_Be_Able_To_Navigate_To_Add_A_Computer_Screen()
{ 
  WebBrowser.Navigate().GoToUrl("http://computer-database.herokuapp.com/computers");
  WebBrowser.FindElement(By.Id("add")).Click();
  var addComputerPageHeading = WebBrowser.FindElement(By.Id("main")).FindElement(By.CssSelector("h1")).Text;

  Assert.IsTrue(addComputerPageHeading.Equals("Add a computer"));
}


### Taking things further

This has been a really basic example of getting started, as you begin to add more and more tests around your web application you will want to start looking at creating re-usable helper objects for your tests to make them a little easier to maintain. 
