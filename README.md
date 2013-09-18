# Wireless Config
A 802.1x configuration suite for Mac OS X
Currently This suite is in testing

# Contributing code

### Fork the repository to your github account
__Click the little fork button in the right hand corner and choose your username__

### Clone your fork of the tool
`git clone https://yourusername@github.com/yourusername/WirelessConfig.git`

~~~
Cloning into WirelessConfig...
Password: 
remote: Counting objects: 361, done.
remote: Compressing objects: 100% (188/188), done.
remote: Total 361 (delta 159), reused 348 (delta 146)
Receiving objects: 100% (361/361), 5.49 MiB | 861 KiB/s, done.
Resolving deltas: 100% (159/159), done.
~~~

`wifiutil.py`
Is a 10.5,10.6,10.7 Wireless configuration command line tool

example usage:
```shell
sudo ./wifiutil.py --username=bob --password=f00b4r --plist='/path/to/wifiutil.settings.plist'
```
or debug:
```shell
sudo ./wifiutil.py --username=bob --password=f00b4r --plist='/path/to/wifiutil.settings.plist' -d
```

This script has support for removal and addtion of WPA2E networks.
Technically it has support for WPA too but this only works really well on 10.6+

WirelessConfig.bundle:
A Casper self service plugin, see this document for scoped installation:

https://jamfnation.jamfsoftware.com/article.html?id=177

Otherwise you can upload through the JSS portal but not recommended while this in Beta.

`kcutil`:
A keychain binary because 10.5 is stupid and I hate it, please upgrade.

wifiutil.settings.plist:
Two arrays, to add and remove networks
Note this is excluded from the build process, check the downloads section for examples
This file MUST BE EDITED for your env settings. Its in the .bundle, so right click
and "Show Package Contents" from there its ./Contents/Resources/wifiutil.settings.plist


To Do:
* Currently the script requires trusted Certificates be configured through
some other process. This will eventually be embeded in a future release.

* This is currently PEAP centric (plist key 25) but needs further testing with other
parameters ,including multiple authentication options.

* Need to get the protocol declaration right so Xcode stops complaining

* networksetup may prompt for password on 10.7, some rootObject auth deal

* Figure out why I am having to rely so heavly on bindings and properties for ui changes:

http://stackoverflow.com/questions/9238178/stringvalue-not-working-on-nstextfield-when-linked-via-files-owner-implemented

http://stackoverflow.com/questions/9639370/counting-the-length-of-two-nstextfields-not-working

Both issues are already worked around but I'm curious why this is this way

* Modify the code to pass the ENV vars to the command as parameters is not as secure.

Beta Notes:

Please Make sure to modify your wifiutil.settings.plist with new guids, here is an example of how to generate them
```shell
sand-bender:~ acid$ uuidgen | tr '[:upper:]' '[:lower:]'
36afb32f-ee45-46e1-9aa8-8a58d013acad
sand-bender:~ acid$ uuidgen | tr '[:upper:]' '[:lower:]'
3ca519d7-98f2-4f50-b0d2-370473b71985
sand-bender:~ acid$ uuidgen
8A1E81A7-170B-466C-B2B2-BF8209AFF994
sand-bender:~ acid$ uuidgen
84E74439-A169-423B-A509-59EC1A0A2679
```
These are used for the profile thats created and the keychain items so they should be unique.

Please look through ALL the keys, I will upload a key value guide in the future, but for the moment

please just find and replace SSID and org name, other keys are written directly to plist so modify

with caution. Example is setup for PEAP (key 25) and a ssid called "newNetwork"

Note that newNetwork is listed in the remove and the add, so that password changes can happen

