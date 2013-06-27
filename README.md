XPrivacy
========

The ultimate, yet easy to use, privacy manager for Android

Index
-----

* [Description](https://github.com/M66B/XPrivacy#description)
* [Features](https://github.com/M66B/XPrivacy#features)
* [Restrictions](https://github.com/M66B/XPrivacy#restrictions)
* [Limitations](https://github.com/M66B/XPrivacy#limitations)
* [Installation](https://github.com/M66B/XPrivacy#installation)
* [Upgrading](https://github.com/M66B/XPrivacy#upgrading)
* [Usage](https://github.com/M66B/XPrivacy#usage)
* [Permissions](https://github.com/M66B/XPrivacy#permissions)
* [Frequently asked questions](https://github.com/M66B/XPrivacy#frequently-asked-questions)
* [Support](https://github.com/M66B/XPrivacy#support)
* [Changelog](https://github.com/M66B/XPrivacy#changelog)
* [Similar solutions](https://github.com/M66B/XPrivacy#similar-solutions)
* [Contributing](https://github.com/M66B/XPrivacy#contributing)
* [License](https://github.com/M66B/XPrivacy#license)

Description
-----------

XPrivacy can prevent applications (including associated background services and content providers)
from leaking privacy sensitive data.
XPrivacy can restrict the categories of data an application can access.
This is done by feeding an application with no or fake data.
There are several data categories which can be restricted, for example *contacts* or *location*.
For example, if you restrict access to contacts for an application,
this will result in sending an empty contact list to the application if it requests access to your contacts.
Similarly, restricting an application's access to your location
will result in a random location being sent to the application.

XPrivacy doesn't revoke (i.e. block) permissions from an application,
which means that most applications will continue to work as before and won't force close.
There are two exceptions to this, access to the internet and to external storage (typically an SD card)
is restricted by denying access (revoking permissions).
There is no other way to realize this, since these permissions are handled by Android in a special way.
Android delegates handling of these permission to the underlying Linux network/file system.

If restricting a category of data for an application results in problems for that application,
it is possible to allow access to the data category again.

By default, all newly-installed applications will have no access to any data category at all,
to prevent a new application from leaking sensitive data after installation.
Shortly after installing a new application,
XPrivacy will ask which data categories you want the new application to have access to.
XPrivacy comes with an application browser,
which allows you to quickly enable or disable applications' access to a particular data category
(i.e. to view and control all access to the camera, for example).

To help you identify potential data leaks,
XPrivacy will monitor attempts made by all applications to access sensitive data.
XPrivacy will highlight (with a yellow triangle) a data category for an application
(or an application name in the application browser)
as soon as data of the data category has been used.
XPrivacy will also display if an application has internet access,
indicating that the application poses a risk of sharing the data it obtains with an external server.
If an application has requested Android permissions to access data in a data category,
it will also be displayed (with a green tick),
but this will only be shown when looking at an individual application,
since checking permissions for all applications is quite slow.

XPrivacy is built using the [Xposed framework](http://forum.xda-developers.com/showthread.php?t=1574401).
XPrivacy taps into a number of selected functions of Android through the Xposed framework.
Depending on the function, XPrivacy conditionally skips execution of the original function
(for example when an application tries to set a proximity alert)
or alters the result of the original function (for example to return empty calendar data).

XPrivacy has been tested with CyanogenMod 10 and 10.1 (Android 4.1 and 4.2),
and will likely work with any Android version 4.1 or 4.2 variant, including stock ROMs.
Root access is needed to install the Xposed framework.
Because of a bug in the Xposed framework, XPrivacy currently needs a fixed Xposed binary,
which is provided as download for both Android version 4.1 and 4.2.


**XPrivacy was a lot of work, so please support this project**

Donate a few dollars for the [pro version](http://www.faircode.eu/xprivacy/)

or

buy [the pro enabler](https://play.google.com/store/apps/details?id=biz.bokhorst.xprivacy.pro) in Google Play

or

[![Flattr](http://api.flattr.com/button/flattr-badge-large.png "Flattr This!")](http://flattr.com/thing/1491130/ "The ultimate, yet easy to use, privacy manager")


**Using XPrivacy is entirely at your own risk**

![Xposed](https://raw.github.com/M66B/XPrivacy/master/screenshots/xposed.png)
![Applications](https://raw.github.com/M66B/XPrivacy/master/screenshots/applications.png)
![Application](https://raw.github.com/M66B/XPrivacy/master/screenshots/application.png)
![Expert](https://raw.github.com/M66B/XPrivacy/master/screenshots/expert.png)
![Help](https://raw.github.com/M66B/XPrivacy/master/screenshots/help.png)
![Settings](https://raw.github.com/M66B/XPrivacy/master/screenshots/settings.png)

Features
--------

* Simple to use
* No need to patch anything (no source, no [smali](https://code.google.com/p/smali/) or anything else)
* For any (stock) variant of Android version 4.1 or 4.2 (JellyBean)
* Newly installed applications are restricted by default
* Displays data actually used by an application
* Open source

Restrictions
------------

For easy usage, data is restricted by category:

* Accounts
	* return an empty account list
	* return fake account info
	* return empty authorization tokens
* Boot
	* prevent applications to start during device startup
* Browser
	* return an empty bookmark list
	* return empty search history
* Calendar
	* return an empty calendar
* Calling
	* prevent calls from being placed
	* prevent SMS messages from being sent
	* prevent MMS messages from being sent
	* prevent data messages from being sent
* Contacts
	* return an empty contact list
* Identification
	* return a fake Android ID
	* return a fake device serial number
* Internet
	* revoke access to the internet
* Location
	* return a random or set location
	* return empty cell location
	* return an empty list of (neighboring) cell info
	* prevents proximity alerts from being set
	* prevents sending NMEA data to an application
	* prevent phone state from being sent to an application
		* Cell info changed
		* Cell location changed
* Media
	* prevent recording audio (including from the microphone)
	* prevent taking pictures
	* prevent recording video
	* you will be notified if an application tries to perform any of these actions
* Messages
	* return an empty SMS/MMS message list
	* return an empty list of SMS messages stored on the SIM (ICC SMS)
	* return an empty list of voicemails
* Network
	* return fake IP's
	* return fake MAC's (network, Wi-Fi, bluetooth)
	* return fake BSSID/SSID
	* return an empty list of Wi-Fi scan results
	* return an empty list of configured Wi-Fi networks
	* return an empty list of bluetooth devices
* Phone:
	* return a fake own/in/outgoing/voicemail number
	* return a fake subscriber ID
	* return a fake phone device ID
	* return a fake ISIM/ISIM domain
	* return a fake IMPI/IMPU
	* return a fake MSISDN
	* return fake mobile network info (country, operator/name)
	* return fake SIM info (serial number, country, operator/name)
	* return empty [APN](http://en.wikipedia.org/wiki/Access_Point_Name) list
	* return no currently used APN
	* return an empty call log
	* return an empty list of voicemail messages
	* prevent phone state from being sent to an application
		* Call forwarding indication
		* Call state changed (ringing, off-hook)
		* Mobile data connection state change / being used
		* Message waiting indication
		* Service state changed (service/no service)
		* Signal level changed
* Storage
	* revoke permission to the external storage (SD card)
* Shell
	* Linux shell
	* Superuser shell
	* Load/library
* System
	* return an empty list of installed applications
* View
	* prevent links from opening in the browser
	* you will be notified if an application tries to open a link

Limitations
-----------

* Android can be restricted, but there will be no usage data available (orange triangles)

Installation
------------

It seems like a lot of steps, but it is done in no time:

1. Requirement: Android 4.1+ (JellyBean), check with *System Settings* > *About phone* > *Android version*
1. **Make a backup**
1. If not done already: root your device; the procedure depends on the brand and model of your device
1. Enable *System settings* > *Security* > *Unknown sources*
1. Install the [Xposed framework](http://forum.xda-developers.com/showthread.php?t=1574401)
	* Be sure to follow all installation steps
	* Be sure to install the latest version 2.1.4
	* Download and copy the Xposed disabler to your SD card to disable Xposed in case of troubles
	* [MIUI](http://en.miui.com/) is not supported by Xposed
1. Install XPrivacy from [here](http://goo.im/devs/M66B/xprivacy)
	* Alternatively download from [here](http://d-h.st/users/M66B/?fld_id=19078#files)
1. Enable XPrivacy from the Xposed installer
1. Reboot into recovery
1. Flash the Xposed fix for your Android version from [here](http://goo.im/devs/M66B/xprivacy)
	* Android 4.1.x / CM10: Xposed_fix_4.1.zip
	* Android 4.2.x / CM10.1: Xposed_fix_4.2.zip
	* **This fix is only for Xposed version 2.1.4**
	* Alternatively download from [here](http://d-h.st/users/M66B/?fld_id=19078#files)
1. Reboot

I do not recommend using XPrivacy in combination with any of the
[similar solutions](https://github.com/M66B/XPrivacy#similar-solutions),
because it will most probably result in conflicts (with as possible consequence data leakage).

Upgrading
---------

* **Make a backup**
* Install the new version (replacing the previous version)
* Reboot your device

You can check for updates using the options menu.
If there is an update the browser will download it.

Usage
-----

1. Start XPrivacy
2. Select a data category at the top, for example *Accounts*
3. Restrict data of the selected data category for an application by ticking a check box
4. Tap on the application icon to see the restrictions for all categories for the application
5. Tap on the application icon to start the application to test (after previous step)

To see it in action: try restricting the category *Identification* for
[Android Id Info](https://play.google.com/store/apps/details?id=com.bzgames.androidid)
or try restriction the category *Contacts* for the Contacts application
(the Contacts application will continue to show a spinner, which is actually a bug in the Contacts application).

**Applying some restrictions requires restarting applications and/or your device**

If an application requested Android permissions for a data category,
the category will be marked with a green check mark icon.
If an application used/tried to use data, the data category will be marked with an orange triangle icon.
These icons are just a guideline, because an application can access privacy sensitive data without Android permissions,
for example the serial number of your device
and because is not possible to monitor data usage in each and every situation,
for example not for access to the internet or the external storage.

Enabling internet or storage restriction means blocking access to the internet
or to the external storage (typically the SD card).
This may result in error messages and even in forced closes of the application.

**Using XPrivacy is entirely at your own risk**

Permissions
-----------

XPrivacy asks for the following Android permissions:

* Internet: to check for updates (only manual from the menu)
* Storage: to export settings to the SD card (only [pro version](http://www.faircode.eu/xprivacy/))

If you don't like this, you can always restrict XPrivacy itself ...

Frequently asked questions
--------------------------

**(1) Will XPrivacy make my device slower?**

Maybe a little bit, but it will probably not be noticeable.

**(2) Does XPrivacy use a lot of memory or battery?**

Almost nothing.

**(3) Can you help me with rooting my device?**

There are already enough guides to help you to root your device.
Use your favorite search engine to find one.

**(4) Do I really need to install the Xposed fix?**

If you like to have all data restricted, yes.
The current Xposed version cannot hook all functions with the same name having different parameters,
like *requestLocationUpdates* of [LocationManager](http://developer.android.com/reference/android/location/LocationManager.html).

**(5) How can I reset all XPrivacy settings?**

*Manage apps* > *XPrivacy* > *Clear data*

**(6) Can I backup XPrivacy and settings?**

Yes, you can, for example with [Titanium backup](https://play.google.com/store/apps/details?id=com.keramidas.TitaniumBackup),
but you can only restore onto the same device.
Exporting/importing settings will work across devices.
To export/import settings you will need the [pro version](http://www.faircode.eu/xprivacy/).

**(7) What is expert mode?**

In expert mode you will be able to block applications from starting at device boot time,
restrict shell access for applications (including super user)
and restrict system applications, including Android itself. **Be careful!**
Furthermore you will be able to make exceptions for individual functions within a restriction category.

**(8) Will you block the iptables command or force online state?**

Maybe in a later stage.

**(9) Will you make it possible to enter fake data?**

Maybe in a later stage.
For now I like to keep things as simple as possible for maximum stability.
Since version 0.21 you can enter a fake location.
Since version 0.30 you can enter a fake MAC address.

**(10) Which functions are exactly restricted?**

Many, see [here](https://github.com/M66B/XPrivacy/blob/master/src/biz/bokhorst/xprivacy/XPrivacy.java) for all details.

**(11) What did you fix in the Xposed framework?**

See [here](https://github.com/M66B/Xposed/commit/8a46f91bfd1381f78d1deb575041f51bae5d3dda).

**(12) How safe is XPrivacy?**

Great care is taken to develop XPrivacy, nevertheless data could leak, although nobody has reported any data leak so far.
So far no critical bugs have been reported.

**(13) Why is XPrivacy not in the Play store?**

Google will probably remove XPrivacy from the Play store eventually,
since it will be able to block advertisements (for example by revoking internet permissions).

**(14) I get 'Incompatible ...' !**

A check of XPrivacy failed, resulting in potential data leakage.
Please report the exact message in the XDA thread,
stating the device and ROM you are using.

**(15) Do I need to install Xposed/the fix again when I install an update of my ROM?**

Yes, mostly you will have to.
XPrivacy will warn you when Xposed isn't installed,
the wrong version of Xposed is installed
or when the XPrivacy is not enabled in Xposed.

**(16) Can I restrict an application with root access?**

Yes, you can, but the application could circumvent anything, since root access means it can do anything it likes.
Nevertheless the application was probably not built to circumvent everything this way.
Version 0.26 will allow you to restrict shell access for any application, which effectively means revoking root access.

**(17) Will restrictions be applied immediately?**

It can take up to 15 seconds before changes in restrictions will be effective, because of caching.
Changing the internet and storage restriction requires an application restart.
Please note that in many cases pressing *back*, only moves the application to the background.

**(18) Can XPrivacy ask for restrictions on demand?**

It cannot always, since it works deep within Android,
and therefore it is IMHO not a good idea to ask for restrictions when it could,
because this will probably only result into confusion.

Newly installed applications are by default fully restricted.
Restricting an application should not result into any force close (crash),
please create an issue if this happens (see for support below),
it only means that an application cannot see the restricted data.
If an application should see the data, you can remove the associated restriction at any time.

**(19) Does XPrivacy have a firewall?**

Yes, you can restrict internet access for any application.
If you want to partly enable internet, for example for Wi-Fi only,
you will have to use a firewall application, like [AFWall+](http://forum.xda-developers.com/showthread.php?t=1957231).
The reason is that XPrivacy works within Android
and that detailed firewall rules can only be applied within the Linux kernel.

**(20) Could you ... with Android permissions?**

Android permissions do not cover all restriction categories and if they do, then mostly only partly.
Therefore Android permissions are only displayed as a guideline.
Any function, like filtering and selecting, would be inherent incorrect.

**(20) I get 'Unable to parse package'**

This means the downloaded app is corrupt.
Try disabling your popup blocker or download using another computer.

Support
-------

*Before submitting any issue please ensure you are running the latest version of XPrivacy.*

If you encounter any bug or data leakage please [report an issue](https://github.com/M66B/XPrivacy/issues),
preferably including a [logcat](http://developer.android.com/tools/help/logcat.html)
(use [pastebin](http://pastebin.com/) or a similar service).

If you have a feature request, please [create an issue](https://github.com/M66B/XPrivacy/issues),
but check if there doesn´t already exist a similar request.

If you have any question, you can leave a message in the [XDA XPrivacy forum thread](http://forum.xda-developers.com/showthread.php?p=42488236).

Changelog
---------

**Version 0.37** (in development)

* Use fastscroll on app list (thanks @[Tungstwenty](https://github.com/Tungstwenty))
* Add actions to app option menu: Lauch app, Settings, Play Store (thanks @[Tungstwenty](https://github.com/Tungstwenty))

**Version 0.36**

* Forgot to remove debug code

**Version 0.35**

* Speed up import ([pro version](http://www.faircode.eu/xprivacy/) only) ([issue](https://github.com/M66B/XPrivacy/issues/70))
* Remove pro menu when pro version activated
* Send support information for detected incompatibilities ([issue](https://github.com/M66B/XPrivacy/issues/82), [issue](https://github.com/M66B/XPrivacy/issues/83))
* Fix potential account data leak ([issue](https://github.com/M66B/XPrivacy/issues/75))
* Fix potential resource leak in location listener
* Updated German translation
* Updated simplified Chinese translation

**Version 0.34**

* Show edit icon in category browser

**Version 0.33**

* Option to switch between light/dark theme

**Version 0.32**

* Move *Shell* category to expert mode
* Export/import function restrictions ([pro version](http://www.faircode.eu/xprivacy/) only)
* Ongoing notification while exporting/importing
* Added link to restrictions in help
* Prevent application details reached from notification to show up in recent
* Added Japanese translation

**Version 0.31**

* Show storage folder in about
* Support for XPrivacy Pro from Google Play
* Fix Skype crash ([issue](https://github.com/M66B/XPrivacy/issues/50))

**Version 0.30**

* Option to set MAC address
* Workaround Skype crash ([issue](https://github.com/M66B/XPrivacy/issues/50))
* Fixed notification for uninstalled apps ([issue](https://github.com/M66B/XPrivacy/issues/51))
* Attemp to fix initial lag ([issue](https://github.com/M66B/XPrivacy/issues/59))
* Added Romanian translation

**Version 0.29**

* Fix initial display of restrictions

**Version 0.28**

* Fixed wrong usage data in app list

**Version 0.27**

* Register more usage data (orange triangle)
* Display time of last usage (application restriction details)
* Highlight system applications (in expert mode)
* New expander symbol
* Menu *All* in application details to toggle all check boxes
* Action bar navigate up ([issue](https://github.com/M66B/XPrivacy/issues/12))
* Refresh application list when toggling expert mode
* Basic application search/filter ([issue](https://github.com/M66B/XPrivacy/issues/13))
* Added French translation
* Added Slovak translation
* Added simplified Chinese translation
* Updated Greek translation

**Version 0.26**

* Restrict process builder (shell, superuser) ([issue](https://github.com/M66B/XPrivacy/issues/44))

**Version 0.25**

* Fixed network usage data
* Fixed text wrapping application info
* Fixed to strict network restrictions (network state available now)
* Fixed to strict system restrictions (start activity available now)
* Fixed multiple installation notifications ([issue](https://github.com/M66B/XPrivacy/issues/42))
* Restrict bluetooth MAC / devices
* More compatibility checks
* Granular restrictions in expert mode only
* Hide indicator when no functions in restriction group
* Start application from application details icon
* Restrict shell commands, including superuser
* Restrict loading libraries (category shell)

**Version 0.24**

* Display application version
* More granular restrictions
* Restrict system properties:
	* ro.gsm.imei
	* net.hostname
	* ro.boot.serialno
	* ro.boot.wifimacaddr
	* ro.boot.btmacaddr
	* Let me know if there more should be restricted
* Fixed location battery drain bug ([issue](https://github.com/M66B/XPrivacy/issues/38))

**Version 0.23**

* Location range check
* Other location input method
* Simplified user interface
* Added Hebrew translation

**Version 0.22**

* Renamed category *Actions* to *Calling* again
* Moved opening links to new category *View*
* Export/import settings, like expert, location (export/import features [pro version](http://www.faircode.eu/xprivacy/) only)

**Version 0.21**

* Settings for latitude/longitude (Christmas Island is at latitude -10.5, longitude 105.667)
* Undo existing restrictions for apps when importing restrictions (only for apps with exported settings)

**Version 0.20**

* Consider XPrivacy as system app (for expert mode)
* Fixed category browser ([bug](https://github.com/M66B/XPrivacy/issues/30), [fix](https://github.com/M66B/XPrivacy/pull/28))
* Notify when new application installed ([feature request](https://github.com/M66B/XPrivacy/issues/10))
* Notify when new system application is installed in expert mode (default allow)

**Version 0.19**

* More environment checks when starting
* More privacy (fallback procedure when low memory)

**Version 0.18**

* Basic check for updates (manually)
* Link to [pro version](http://www.faircode.eu/xprivacy/)
* Renamed category *Calling* to *Actions* and moved opening browsers links into this category

**Version 0.17**

* User interface improvements
* Display system apps in expert mode only
* Restrict opening links ([issue](https://github.com/M66B/XPrivacy/issues/15))
* Restrict serial number (system/build properties)
* Export/import ([issue](https://github.com/M66B/XPrivacy/issues/18)) ([pro version](http://www.faircode.eu/xprivacy/) only)

**Version 0.16**

* Removed XPrivacy from *Manage apps*
* Added application list to XPrivacy

**Version 0.15**

* Restrict Android (expert mode)
* Restrict Google Service Framework (see also [limitations](https://github.com/M66B/XPrivacy#limitations))
* Restrict Wi-Fi BSSID, IP and SSID
* Restrict network info
* No default deny for updated apps

**Version 0.14**

* Restrict calling (untested)
* Restrict sending SMS
* Restrict sending MMS (untested)
* Fix setting restrictions in the app list

**Version 0.13**

* Internet restriction (revoke permission)
* Remove restrictions/audit trail when uninstalling an app
* Custom write permission for privacy provider
* Restriction caching (Play store installed app browse should be fast again)

**Version 0.12**

* Android version check
* Check if XPrivacy is enabled
* Async app list fetch
* Several user interface improvements
* Expert mode: prevent app start
* Added Dutch/Flemish translation
* Added Bulgarian translation, thanks [borislavba](https://github.com/borislavba)
* Added German translation, thanks [NosferatuAlucard](https://github.com/NosferatuAlucard)
* Added Greek translation, thanks [mikeNG](https://github.com/mikeNG)
* Added Slovenian translation, thanks [kv1dr](https://github.com/kv1dr)

Similar solutions
-----------------

* [PDroid](http://forum.xda-developers.com/showthread.php?t=1357056)
* [PDroid 2.0](http://forum.xda-developers.com/showthread.php?t=1923576)
* [OpenPDroid](http://forum.xda-developers.com/showthread.php?t=2098156)
* [LBE Privacy Guard](https://play.google.com/store/apps/details?id=com.lbe.security.lite)
* [CyanogenMod Incognito Mode](https://plus.google.com/100275307499530023476/posts/6jzWcRR6hyu)
* [Per App Settings Module](http://forum.xda-developers.com/showthread.php?t=2072081)

The *PDroid* family provides fake or no data, more or less in the same way as XPrivacy does.
A difference is that you need to patch Android and that there is (therefore) only limited stock ROM support.
The PDroid family is open source.

*LBE Privacy Guard* revokes permissions, which will make some applications unusable.
LBE Privacy Guard also features malware protecting and data traffic control.
Some consider the closed source code of Chinese origin as a problem.

The members of the PDroid family and XPrivacy hardly use memory, but LBE Privacy Guard does.

The CyanogenMod Incognito Mode seems not to be fine grained and provides only privacy for personal data,
if the associated content provider chooses to do so.

The *Per App Settings Module* revokes permissions like LBE Privacy Guard does.

Contributing
------------

Translations:

* Translate the strings in [this file](https://github.com/M66B/XPrivacy/blob/master/res/values/strings.xml)
* Send the translated file to me [via an XDA PM](http://forum.xda-developers.com/member.php?u=2799345)

Current translation:

* English
* Bulgarian (bg)
* German (de)
* Greek (el)
* French (fr)
* Hebrew (he/iw)
* Japanese (ja)
* Dutch/Flemish (nl)
* Romanian (ro)
* Slovak (sk)
* Slovenian (sl)
* Simplified Chinese (zh-rCN)

Restrict new data:

* Find the package/class/method that exposes the data (look into the Android documentation/sources)
* Figure out a way to get a context (see existing code for examples)
* Create a class that extends [XHook](https://github.com/M66B/XPrivacy/blob/master/src/biz/bokhorst/xprivacy/XHook.java)
* Hook the method in [XPrivacy](https://github.com/M66B/XPrivacy/blob/master/src/biz/bokhorst/xprivacy/XPrivacy.java)
* Write a before and/or after method to restrict the data
* Do a [pull request](https://help.github.com/articles/using-pull-requests) if you want to contribute

Contributors do not have to donate for the [pro version](http://www.faircode.eu/xprivacy/).

License
-------

[GNU General Public License version 3](http://www.gnu.org/licenses/gpl.txt)

Copyright (c) 2013 [Marcel Bokhorst](http://blog.bokhorst.biz/about/)
([M66B](http://forum.xda-developers.com/member.php?u=2799345))

This file is part of XPrivacy.

XPrivacy is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

XPrivacy is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with XPrivacy.  If not, see [http://www.gnu.org/licenses/](http://www.gnu.org/licenses/).
