<!--
# license: Licensed to the Apache Software Foundation (ASF) under one
#         or more contributor license agreements.  See the NOTICE file
#         distributed with this work for additional information
#         regarding copyright ownership.  The ASF licenses this file
#         to you under the Apache License, Version 2.0 (the
#         "License"); you may not use this file except in compliance
#         with the License.  You may obtain a copy of the License at
#
#           http://www.apache.org/licenses/LICENSE-2.0
#
#         Unless required by applicable law or agreed to in writing,
#         software distributed under the License is distributed on an
#         "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
#         KIND, either express or implied.  See the License for the
#         specific language governing permissions and limitations
#         under the License.
-->

Ionic's Webview
======

This plugin is an extension of the [Apache Cordova WKWebView plugin](https://github.com/apache/cordova-plugin-wkwebview-engine). It includes enhancements to resolve some of the issues surrounding XHR requests, along with some DOM exception issues.

This plugin only supports iOS 9 and above and will fall back to UIWebView on iOS 8.

The WKWebView plugin is only used by iOS, so ensure the `cordova-ios` platform is installed. Additionly, the `cordova-ios` platform version must be `4.0` or greater.

Installation Instructions
-------------------

Ensure the latest Cordova CLI is installed:  (Sudo may be required)

```
npm install cordova -g
```

Ensure the `ios` platform has been added:

```
ionic cordova platform ls
```

If the iOS platform is not listed, run the following command:

```
ionic cordova platform add ios
```

If the iOS platform is installed but the version is < `4.x`, run the following commands:

```
ionic cordova platform update ios
ionic cordova plugin save           # creates backup of existing plugins
rm -rf ./plugins            # delete plugins directory
ionic cordova prepare               # re-install plugins compatible with cordova-ios 4.x
```

Install the WKWebViewPlugin:

```
ionic cordova plugin add https://github.com/ghenry22/cordova-plugin-ionic-webview --save
```

**Note:**

If you already had [apache/cordova-plugin-wkwebview-engine](https://github.com/apache/cordova-plugin-wkwebview-engine) install make sure that is removed before using this version.

```
ionic cordova plugin rm cordova-plugin-wkwebview-engine
```


Build the platform:

```
ionic cordova prepare
```

Test the app on an iOS 9 or 10 device:

```
ionic cordova run ios
```




Required Permissions
-------------------
WKWebView may not fully launch (the deviceready event may not fire) unless if the following is included in config.xml:
#### config.xml
```
<allow-navigation href="http://localhost:8080/*"/>
<feature name="CDVWKWebViewEngine">
  <param name="ios-package" value="CDVWKWebViewEngine" />
</feature>

<preference name="CordovaWebViewEngine" value="CDVWKWebViewEngine" />
```

New Settings in this Fork
-------------------
This fork introduces some new capabilities which can be configured in your config.xml.

Set the keyboard appearance to use a dark style (default is false)
```
<preference name="KeyboardAppearanceDark" value="true" />
```

Set the port that the built in webserver will listen on (default is 8080)
If you change the port be sure to also update your allow-navigation href statement to match as mentioned in Required Permissions section above.
```
<preference name="WKPort" value="8534" />
```

Enable wkwebview to run in the background (default is false)
When enabled wkwebview will continue to run in background until the OS suspends it.  You still need a valid reason to be running in the background (like audio or geolocation) this does not "spoof" anything for you just allows the wkwebview to continue processing javascript when in the background until suspended by the OS.  This makes the behaviour in line with the older UIWebview.
```
<preference name="WKEnableBackground" value="true" />
```

Application Transport Security (ATS) in iOS 9
-----------

Cordova CLI 5.4.0 onwards supports automatic conversion of the tags in config.xml to ATS.  This should no longer be an issue at this time.

Apple Issues
-------

The `AllowInlineMediaPlayback` preference will not work on OS versions prior to iOS 10.

Limitations
--------

There are several [known issues](https://issues.apache.org/jira/issues/?jql=project%20%3D%20CB%20AND%20labels%20%3D%20wkwebview-known-issues) with the official Cordova WKWebView plugin. The Ionic team thinks we have resolved several of the major issues. Please [let us know](https://github.com/driftyco/cordova-plugin-wkwebview-engine/issues) if something isn't working as expected.

This fork contains further fixes for numerous issues that I have come across.  I will be doing my best to actively maintain this plugin and test and merge in any suggested fixes or PR's contrinbuted by the community.  Hopefully this can provide a faster moving repository for the wkwebview work that the ionic team started.
