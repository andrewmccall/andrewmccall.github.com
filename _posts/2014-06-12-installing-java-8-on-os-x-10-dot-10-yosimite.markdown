---
layout: post
title: "Installing Java 8 on OS X 10.10 Yosimite"
date: 2014-06-12 21:36:55 +0100
comments: true
categories: 
- Java
- Java 8
---

So I've been running OS X 10.10 for a while and tonight decided I'd try to install the Java 8 JDK (JDK8u05)  and have a play for a project I've been messing around with. Unfortunately I got this: 

![Fail](/images/post_images/java8u05-osx-10.10-install-fail.png)

A quick google search and the best I could come up with was to install the latest beta of OpenJDK, which apparently fixes the problem. I didn't really want a beta version of the JDK so I had a dig around in the pkg to see if I could force the installations. 

The checks for versions are just in a text file within the package, so it's not hard to remove the check and force the installation.

First expand the pkg into a directory so you can get at the contents: 

`$ pkgutil --expand JDK\ 8\ Update\ 05.pkg JDK8`

This creates a new folder called JDK8, in there you'll find a file called `Distribution`. Open it in your favourite text editor. At about line 36 you'll find the following code: 

```js linenos:true start:36
// Check is current MAC OS X version less than supportedVersion
function checkForMacOSX(supportedVersion) {
    try {
        // Get current ProductVersion
        var tProductVersion = system.version.ProductVersion;
        // Get current ProductName
        var tProductName = system.version.ProductName;

        // Check if current version is less than supportedVersion, if yes Set the result type to Fatal, and give correct message to user

        if(tProductVersion &lt; supportedVersion)
        {
            // Set result values
            var osCheckTitle = system.localizedStringWithFormat('OSCHECK_TITLE');
            osCheckTitle = osCheckTitle.replace("%1$@", tProductName);
            osCheckTitle = osCheckTitle.replace("%2$@", supportedVersion);
    
            var osCheckMessage = system.localizedStringWithFormat('OSCHECK_MESSAGE');
            osCheckMessage = osCheckMessage.replace("%1$@", tProductName);
            osCheckMessage = osCheckMessage.replace("%2$@", tProductVersion);
            osCheckMessage = osCheckMessage.replace("%3$@", supportedVersion);
    
            my.result.title = osCheckTitle;
            my.result.message = osCheckMessage;
            my.result.type = 'Fatal';
        }
    } catch (e) {
        // an exception just occurred
        return (false);
    }
    // return true
    return (true);
}
```

The error happens on line 45 above, the version check is comparing strings and failing because 10.10 is less than 10.7 lexicographically. If I was fixing the pkg I would rewrite the function to properly check, but I'm not and I just want the JDK to install. So I took everything out except the final `return(true);` so that the whole method looks like this: 

``` js start:36 
// Check is current MAC OS X version less than supportedVersion
function checkForMacOSX(supportedVersion) {
    // return true
    return (true);
}
```

Finally package it back up with the `pkgutils` command and the check won't fail and Java 8 will install.

`$ pkgutil --flatten JDK8 JDK8.pkg`

Double click the new pkg and the installer will run without the error message.

![Success](/images/post_images/java8u05-osx-10.10-install-success.png)

All done, Java 8 JDK installed!


