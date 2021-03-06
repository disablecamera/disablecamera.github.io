---
layout: page
title: Permanently Disable Camera
---

**[Permanently Disable Camera](https://play.google.com/store/apps/details?id=com.disablecamera)**
is an app for Android 5.0 or later that disables the camera(s) on your Android
phone or tablet. Unlike other camera-disabling apps
([Cameraless](https://play.google.com/store/apps/details?id=com.manyera.simplecameradisable),
 [Camera Block](https://play.google.com/store/apps/details?id=com.bettertomorrowapps.camerablockfree),
 etc.), this app lets you disable the camera in a way that **cannot be reversed,
not even by you**. It requires some manual setup steps, described below.

See the [FAQ](/faq) for more information.

# Instructions

After you install the app and go through its steps to disable the camera, you'll
need to go through a number of additional manual steps to make it permanent.

You'll need:

* An Android phone or tablet running Android 5.0 (Lollipop) or later.
* A computer where you can install the Android developer tools.
* A USB cable to plug your Android device into your computer.

# 1. Install the app and disable the camera

There are two ways to install the app:

* Visit the [Google Play Store listing](https://play.google.com/store/apps/details?id=com.disablecamera)
  for the app and install it from there.
* If you can't install the app from the Play Store, you can instead click this
  [direct download link](/downloads/permanently-disable-camera-1.2.apk) to
  directly download the app as an APK file. You will likely need to change your
  settings to allow apps from untrusted sources. See
  [this article](https://www.howtogeek.com/313433/how-to-sideload-apps-on-android/)
  for instructions on how to do that.

Once the app is installed, follow the on-screen steps:

1. Tap the "Grant device admin permission" button. The Android system will show
   an "Activate device administrator?" screen, and you should tap "Activate".
2. Tap the "Disable camera" button. This uses the granted permissions to disable
   the camera.

At this point, the camera on your device will be disabled for all apps. However,
you are still able to re-enable the camera by revoking the permissions you
granted and uninstalling the app. If you want to "freeze" the app to permanently
disable the camera, then continue with these instructions.

Note that after following the full instructions, the app will also apply two
device policies that stop you from creating new users on the device or
performing a factory reset from the settings menu. Both of these policies are
needed to ensure that the cameras cannot be re-enabled.

# 2. Enable USB debugging on your Android device

This configures your Android device to allow you to send commands to it.

In the Settings app:

1. Enable the "Developer options" menu (if you haven't done so) by going to the
   "About phone" (or "About tablet") menu, scrolling to the bottom, and tapping
   "Build number" 7 times. A message will appear saying that you are now a
   developer.
2. In the "Developer options" menu, go to the "USB debugging" option and enable
   it.

See [this YouTube video](https://www.youtube.com/watch?v=pfE6m0iSLbk) for an
example. You may also be able to search the internet for help if you run into
any trouble.

# 3. Set up ADB on your computer

Android Debug Bridge (ADB) is a utility included in the Android developer tools
that allows you to send commands to your Android device, and you'll need it to
"freeze" the app so that it cannot be uninstalled.

The full way to install ADB is to install the
[Android SDK](http://developer.android.com/sdk), then open "Android SDK Manager"
and install "Android SDK Platform-tools". That should install the `adb` command
that you can run from a command line.

There are also alternative ways that may be simpler, like in these explanations:

* [Windows setup YouTube video](https://www.youtube.com/watch?v=0ccUcPR2Mko)
* [Mac/Linux setup YouTube video](https://www.youtube.com/watch?v=5J-UKA87s_o)

When ADB is set up, plug your Android device into your computer and run the
`adb devices` command from a command line. If everything was successful, you'll
see something like this:

~~~
$ adb devices
List of devices attached
WS6X7581AM	device
~~~

If `adb devices` gives an error, then then it wasn't installed successfully. If
it just shows "List of devices attached" without anything below it, then make
sure USB debugging from step 2 is enabled and that your device is connected.

Installing ADB is a common task, so if you run into trouble you should be able
to find help on the internet.

## 4. Temporarily remove all accounts from your Android device

Now that ADB is set up, you'll use it to set the Permanently Disable Camera app
as a "device owner" so it can't be uninstalled. But doing so requires that your
Android device not have any accounts associated with it (most notably Google
accounts, but also other accounts like Facebook and Twitter that are registered
as accounts on the device), so you'll need to remove them for now.

In the Settings app, go to the "Accounts" menu. For each account, tap the menu
button in the top right and tap "Remove account". It will display a warning that
all messages, contacts, and other data will be deleted from the device. This is
generally not a big deal; any messages, contacts, etc will be re-added when you
add the accounts back in the last step, so in typical situations you won't lose
any data. You may want to write down which accounts you removed so you can add
them back in the last step.

Also, if you have other users on the device (e.g. a guest user), you need to
remove them as well. To remove the guest user, you can switch to the guest user
using the user menu, then when you go back to the user menu there will be a
"Remove guest" button. See
[this YouTube video](https://www.youtube.com/watch?v=gukHgDrq7ZA) for an example
of how to manage users.

Once the device no longer has any accounts or secondary users, you can move to
the next step.

## 5. "Freeze" the app so it cannot be uninstalled

**This is the point of no return.**

Run the following command to set the app as a "device owner" so that it cannot
be uninstalled:

~~~
adb shell dpm set-device-owner com.disablecamera/.AdminReceiver
~~~

You should see a message saying "Success: Device owner set to package
com.disablecamera".

Go back to the Permanently Disable Camera app. It may prompt you to disable the
camera again, in which case you should do so. Then, you should see a message
saying that the camera is permanently disabled. Once you see this message, the
app will also restrict your permissions so that you may not add other users and
so that you may not use the settings option to factory reset the device (since
both of these could be used to re-enable the camera).

If you try to uninstall the app, it will direct you to the device administrators
page, which will not let you revoke permissions for the Permanently Disable
Camera app.

## 6. Add back all accounts to your Android device

Go back to the Settings app, and go to the "Accounts" menu. For each account
that you removed, tap "Add account" and add back. All of your emails, messages,
etc should be added back when the account syncs.

That's it! If you've followed the steps correctly, your Android device should be
just like before, but without a working camera. If you run into any problems,
you may want to see the [FAQ](/faq) for more info.