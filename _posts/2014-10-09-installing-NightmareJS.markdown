---
layout: post
title:  "Installing NightmareJS"
date:   2014-10-09 12:00:00
categories: nodejs
---

[NightmareJS][NightmareJS] provides intuitive [API][NightmareJSAPI] for simple scraping or browser automation on PhantomJS. Install it using NPM:

~~~
F:\nightmare> npm install nightmare
~~~ 

I did encounter some [build issues][BuildIssues] on Windows such as

~~~
C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V110\Microsoft.Cpp.Platform.targets(44,5): error MSB8020: The builds tools for v120 (Platform Toolset = 'v120') cannot be found. To build using the v120 build tools, either click the Project menu or right-click the solution, and then select "Update VC++ Projects...".
~~~ 

This issue is likely due to PhantomJS default use of dnode and weak module which require node-gyp setup with Microsoft VS2010 or [VS2012][VSExpress2012]. Once installed, you can use automation script to browse a site and get its screenshot such as:

~~~
var Nightmare = require('nightmare');
new Nightmare()
  .goto('http://kayak.com')
  .evaluate(function (page) {
    return document.documentElement.innerHTML;
  }, function (res) {
    console.log(res);
  })
  .screenshot('kayak.png')
  .run(function (err, nightmare) {
      if (err) return console.log(err);
      console.log('Done!');
    });
~~~

Do ensure that you have access to `phantomjs.exe` in the nightmare directory before executing following command:

~~~
F:\nightmare> node automation.js
~~~ 

You'll see the HTML codes in the console and get the screenshot image in current directory.

[NightmareJS]:           http://nightmarejs.org/
[NightmareJSAPI]:        https://github.com/segmentio/nightmare#api
[BuildIssues]:           https://github.com/segmentio/nightmare/issues/23
[VSExpress2012]:		 http://www.microsoft.com/en-sg/download/details.aspx?id=34673