---
layout: page
title: FAQ - Permanently Disable Camera
permalink: /faq/index.html
---

# Frequently Asked Questions

**Q: What does "permanent" really mean?**

After you follow the [instructions](/) to “freeze” the app (i.e. set it as a
device owner app), the Android system does not allow the app to have its
permissions revoked or for the app to be uninstalled. This means that the camera
will be disabled with no way to re-enable it.

This is almost as effective as physically destroying the cameras on the phone,
although technically there are ways to use the camera again:

* Reset the device to factory settings. This wipes all accounts, apps, and data
  from the phone.
* If you've rooted your phone, you may be able to use root access to bypass the
  security restrictions and re-enable the camera.

(And, of course, you could buy a new phone.)

**Q: Why would someone want this?**

There are a number of situations where it's useful to have a device without a
working camera (and where the user is not able to re-enable it):

* Individuals may want to avoid having a working camera for various personal
  reasons, like self-control or to establish trust.
* Parents or guardians may want to restrict their children from using the
  camera.
* Corporate/enterprise environments sometimes disallow cameras. This app and
  approach may (or may not) be acceptable proof that your phone does not have a
  working camera. In other situations, it's better for an IT department to come
  up with a more robust solution. See the
  [How it Works](/howitworks) page and the
  [GitHub repo](https://github.com/disablecamera/disablecamera) if you want to
  develop a similar technical solution.

There are also some reasons to disable the camera, even if it's reversible:

* Disabling the camera prevents any possible spyware apps from using the camera.
* Disabling the camera can sometimes fix software issues, like your phone taking
  pictures in your pocket.

**Q: What if I only want to temporarily disable my camera?**

If you disable the camera through the app, but don't follow the instructions to
"freeze" the app, then the camera will be disabled temporarily. To re-enable the
camera, revoke the device administrator permissions for the app.

There are also other apps on the Play Store that disable the camera temporarily,
and some of them have more features.

**Q: Can I use this approach to permanently install other apps?**

Yes, any app that's a Device Administrator app can be set as a device owner
by following the [instructions](/).

You'll need to change the line

~~~
adb shell dpm set-device-owner com.disablecamera/.AdminReceiver
~~~

to use the app's package name instead of `com.disablecamera` and the app's
device admin receiver class instead of `.AdminReceiver`.

**Q: Why is there a "Device may be monitored" message on the notification
shade?**

The Android system always displays this message whenever there is a device owner
app set, and there doesn't seem to be a way to remove it. The message warns
about the *possibility* of monitoring, but the app does not do any monitoring;
it only disables the camera. You can verify this by reading the
[source code](https://github.com/disablecamera/disablecamera).

**Q: Are there any known issues when the camera is disabled?**

* In Android 5.0, disabling the camera also disables the flashlight. This
  appears to be fixed in Android 6.0.
* Older versions of Google Hangouts would crash when trying to join a call. This
  issue appears to be fixed in the latest version.

If you're worried about issues with apps that you use regularly, you may want to
try using your device for a while with the camera temporarily disabled before
following the instructions to disable it permanently.

**Q: I got an error when trying to run the `adb` command. What does it mean?**

Here are some common errors:

`java.lang.IllegalStateException: Trying to set the device owner, but device owner is already set.`

This error means that either the app is already permanently installed, or that
there is already an app permanently installed. An Android device can only have
one app permanently installed in this way.

`java.lang.IllegalStateException: Not allowed to set the device owner because there are already some accounts on the device`

This error means that you need to go to the "Accounts" section of the Settings
app and remove all accounts first. See step 4 in the [instructions](/) for more
details.

`java.lang.IllegalStateException: Not allowed to set the device owner because there are already several users on the device`

This error means that you need to remove all users on the device except the
primary user. See step 4 in the [instructions](/) for more details.

**Q: I changed my mind and want to un-disable the camera. Can you help with
that?**

Sorry, no. Your best option is probably to factory-reset your device.

**Q: What if I have trouble with these instructions or have other questions or
feedback?**

Feel free to email [disablecameradeveloper@gmail.com](mailto:disablecameradeveloper@gmail.com).