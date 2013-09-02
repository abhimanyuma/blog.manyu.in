---
layout: post
title: "[IITK] Getting No Proxy working on your mobile"
tagline: "How to run the authentication script on Android phones"
modified: 2012-09-14
category: tech
tags: [iitk,no-proxy,internet,android,sl4a,firewall-auth.py,python,proxy]
---

**Use this method only if Proxy for Android does NOT work, it is far simpler**

I own a android phone, and no proxy experience sucks for me, and considering that is the only way of connecting to IITK wifi from android , WiFI in IITK sucks for me. Thanks to [Parveen Kumar](http://cse.iitk.ac.in/users/parveenk/) all that has changed, who told me about the method.

No Proxy on laptops is painless due to the following authentication
script, Firewall-auth.py [Link to Repo](https://github.com/sid0/firewall-auth) [Link to Python File](https://raw.github.com/sid0/firewall-auth/631327ae959f132853943acdc62f52b76bea7e8f/firewall-auth.py) Use Save as option to save

In android phone all you now need is a scripting layer, which can run this thing, so the blog will cover the steps.

Before you proceed, be warned, neither me or Parveen takes any responsibility for anything that may happen as a result of this, well except may be if you want to buy us a treat, then go ahead.

*P.S: The painless part refers to when you connect to WiFi, not when you have to set all the instructions below up, but they are ONE time only*.

Pre-requistes : - To do these steps you will need Internet, even GPRS will do,or else you may also try connecting to the WiFi once since usually it works for the first time, through the browser.

If you know how to install a .apk file skip steps 1 and 2.

## 1. Allow non-Market apps to be installed.

The scripting layer is not available in Android market, and hence has to be installed as .apk file. Many of you would have done this, else go to 

> Settings \>\> Application \>\> Unknown Sources. 

Make sure that installing from Unknown sources is allowed.

## 2. APK Installer

If you are directly downloading the application package (.apk file) to your mobile you will not need this, but this is still suggested.

Install this application called [APK Installer](https://play.google.com/store/apps/details?id=com.graphilos.apkinst&feature=search_result#?t=W251bGwsMSwxLDEsImNvbS5ncmFwaGlsb3MuYXBraW5zdCJd) - the link is to Google play, sign in and click install in browser it will automatically download to phone from the market place, what is does is  allows you to browse, the sdcard, and install applications (.apk files) on it.

To install .apk files, just open the app and go to the apk file (In downloads in our case), and click on it.

## 3. SL4A (Scripting Layer for Android)

Basically the script you use on PCs is a python script , to run it on your phone you need two things, a scripting layer, and Python interpreter.

- The Scripting layer can be got at this [link](http://android-scripting.googlecode.com/files/sl4a_r6.apk). You can also know more about this project which is actually much more impressive than our use by [going to their home page](http://code.google.com/p/android-scripting)

- Once you download the link if it is on the phone it should automatically start the installation, else you can use the APK Installer, and go to the location and install it. It will ask for a large number of permissions since it is a general purpose scripting layer.

Now by default you will have only the "Unix Shell" Interpreter installed,  but since our script is in Python we need a python interpreter.

## 4. Python for Android

The simplest way to install it is through SL4A,

- Go to their Options Menu (got by clicking the menu button), select View and Interpreters.
- Now it will show the list of interpreters installed in your phone, usually just the shell. If you find Python 2.X.X among this you are done.
- Otherwise take the options menu again and select Add. Now select python 2.6.2 (Or higher ) from the list.
- This will again download a .apk file to your system.
- Install the .apk file (if it doesn't happen automatically) to your android mobile, just like you installed the scripting layer.
- You may also download it [here](http://code.google.com/p/android-scripting/downloads/detail?name=PythonForAndroid_r4.apk)

## 5. Installing Python Interpreter and Modules

Now you are almost there, the python for android apk only has the base, now go to the "Python for Android" Application that has been installed. This application will take some time to load, and will present only a blank screen initially, and then you will find a list of options,

- Click on the "Install" at the top, and it will start installing the 3 components, this requires about 8 MB of download, so being on the WiFi (which happens for the first 10 minutes) is preferred.
- Now you need to move the [firewall-auth.py](https://raw.github.com/sid0/firewall-auth/631327ae959f132853943acdc62f52b76bea7e8f/firewall-auth.py) file to the folder *sl4a* (on most phones this is in the sd card folder) . This can be done either by connecting the mobile to the computer, or by installing a [file manager](https://play.google.com/store/apps/details?id=com.rhmsoft.fm&feature=search_result)

## 6. Running the script

Now go to the SL4A app, and the file should be listed there, (if not one of the above steps have not been done), just click it and click on the Gear Icon or Terminal Icon that comes. The script will start and stay in the background, you can go back to it by accessing it from the Notification bar.

Comment about any problems/experiences, provided the comment section loads, somehow IITK connection is sometimes refused by Bit.ly and Jetpack(which I use for comments)