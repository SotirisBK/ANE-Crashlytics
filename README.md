Air Native Extension for Crashlytics (iOS + Android)
======================================

This is an [Air native extension](http://www.adobe.com/devnet/air/native-extensions-for-air.html) for [Crashlytics SDK](http://crashlytics.com) on iOS and Android. It has been developed by [FreshPlanet](http://freshplanet.com) and is used in the game [SongPop](http://songpop.fm).


Installation
---------

The ANE binary (AirCrashlytics.ane) is located in the *bin* folder. You should add it to your application project's Build Path and make sure to package it with your app (more information [here](http://help.adobe.com/en_US/air/build/WS597e5dadb9cc1e0253f7d2fc1311b491071-8000.html)).

Before you try to use this ANE, you should first complete the Crashlytics native workflow (iOS or Android) on a test project in order to get your API key. It is linked to your organization and is the same for all your apps, so you only need to do it once.

You will then need to add your API key in your application descriptor twice, once for iOS, once for Android:

* iOS:

```xml
<iPhone>
    
    <InfoAdditions><![CDATA[

        <key>CrashlyticsAPIKey</key>
        <string>{YOUR_API_KEY}</string>

    ]]></InfoAdditions>

</iPhone>
```

* On Android (note the INTERNET permission as well):

```xml
<android>
    <manifestAdditions><![CDATA[
        <manifest android:installLocation="auto">
            
            ...

            <uses-permission android:name="android.permission.INTERNET"/>
            
            ...

            <application>

                ...
                
                <meta-data android:name="com.crashlytics.ApiKey" android:value="YOUR_API_KEY"/>
                
            </application>

        </manifest>
    ]]></manifestAdditions>
</android>
```


Usage
-----

```actionscript
// Start Crashlytics
AirCrashlytics.start();

// Force a crash (iOS only)
AirCrashlytics.crash();

// Set a user identifier
AirCrashlytics.userIdentifier = "myUserIdentifier";

// Set some custom keys
AirCrashlytics.setBool("myBoolKey", true);
AirCrashlytics.setInt("myIntKey", 10);
AirCrashlytics.setFloat("myFloatKey", 2.5);
AirCrashlytics.setString("myStringKey", "myStringValue");
```

In order for crash reports to appear in your dashboard with iOS, you need to execute *tool/run.sh* after building your AIR application. You need to provide the path to your .dSYM file, so if you are compiling in release mode with Flash Builder be sure to check "Keep bin-release-temp folder" otherwise the .dSYM file will be deleted by Flash Builder:

```bash
cd /path/to/the/ane
tools/run.sh CRASHLYTICS_API_KEY PATH_TO_IPA PATH_TO_DSYM
```


Build from source
---------

Should you need to edit the extension source code and/or recompile it, you will find an ant build script (build.xml) in the *build* folder:
    
```bash
cd /path/to/the/ane

# Setup build configuration
cd build
mv example.build.config build.config
# Edit build.config file to provide your machine-specific paths

# Build the ANE
ant
```


Authors
------

This ANE has been written by [Alexis Taugeron](http://alexistaugeron.com). It belongs to [FreshPlanet Inc.](http://freshplanet.com) and is distributed under the [Apache Licence, version 2.0](http://www.apache.org/licenses/LICENSE-2.0).