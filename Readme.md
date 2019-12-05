# Welcome to the Anibis backend developer test

![N|Solid](https://www.anibis.ch/_Frontend/Anibis-Desktop/build/img/anibis-logo.svg)

If you are here, then you received an email with an overview of the process. Here you will find the details of the test.

## Preparation and guidance
* Make sure you implement all acceptance criteria **exactly** as specified (naming matters).
* You can implement the acceptance criteria in whatever order you prefer, but we recommend you to start first with what you know best and feel most comfortable with.
* Open **/src/AnibisBedTest.sln in Visual Studio 2015 or higher**. You will find 2 projects. In each of these projects some functionality should be implemented as described below.
* **You are not allowed to add any more packages, libraries or references to any of the projects** 
* When you're finished, **zip the code and send it to attila.magyar@scout24.ch (exclude packages, bin and obj folder from zip)**. The zip-file should be named anibis-bed-test-[firstname]-[lastname].zip.

**If you cannot finish all tasks, that does not necessarily mean you are out! Complete the tasks as good as you can and then send the test back.**

Let's get to it!

![N|Solid](https://media.giphy.com/media/5ntdy5Ban1dIY/giphy.gif)

## Project LogFileReader
The program should transform the logfile **/src/Data/testdata.log** into an XML file.
* Take the path of the file as a console input parameter
* Perform errorhandling if the file does not exist
* Transform the testdata.log file into an XML file with the following structure:
```
<?xml version="1.0" encoding="UTF-8"?>
<logEntries>
   <logEntry>
      <date>2016-09-23</date>
      <time>08:11:59.853</time>
      <s-sitename>IS24WEBAPI_TEST3</s-sitename>
      <s-computername>VM-INT-ISWEB01</s-computername>
      <s-ip>10.10.180.46</s-ip>
   </logEntry>
</logEntries>
```
* Lines which start with a hash # are comments and can be ignored
* The line which starts with "*#Fields:*" defines the order of the fields in the file (1st column=date, 2nd column=time, etc.). **You can assume that this order will not change through the file**.
* For each line in the logfile, a *logentry* node should be created in the XML and one element per column for each value
* Take only the fields **date, time, s-sitename, s-computername und s-ip** into account. All other fields can be ignored
* The xml file should be **saved under /src/Data/testdata-trans.xml** in the respository and comitted to the repository
* Make sure, that **memory consumption** of the application is low, even if the logfile is very big (e.g. several TB) 

## Project REST-API
The project has **SQLite package already included** as a reference. **Use SQLite with in-memory database** to save data and return that data through the API.
* Find demo code in the internet on how to code with SQLite with C#
* On startup of the REST-API-application: **Create a table news_items** with fields 
  * id INTEGER PRIMARY KEY
  * title VARCHAR(100) NOT NULL
  * content text NULL 
* Populate the table with a few records (5 max) 
* Add a WebAPI-Controller **NewsController with a GET Action** with the route /news which returns the content of the table in JSON format
* Add a **POST action to add new news-items** to the database
* Make sure that the title has a value in a RESTful way (HTTP 400 'Bad Request')