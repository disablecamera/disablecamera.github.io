---
layout: page
title: How it Works - Permanently Disable Camera
permalink: /howitworks/index.html
---

# How it Works

The Permanently Disable Camera app and setup process make use of two Android
concepts: **device administrator apps** and **device owner apps**.

## Device administrator apps

A **device administrator** (see the
[Device Administration](http://developer.android.com/guide/topics/admin/device-admin.html)
docs) is an app that has been given special privileges to set policies on the
device. For example, the app might require you to set a password on your device
or require that your password be a certain length. Starting in Android 4.0, a
device administrator app can disable all cameras on the device. The main use
case for device administrators is enterprise scenarios where an employer wants
to set policies for devices used by employees.

You can view the device administrator apps on your device by going to the
Settings app, tapping "Security", then tapping "Device administrators". Any app
can request permissions to be a device administrator, even ones downloaded from
the Play Store.

However, normal device administrator apps (ones that aren't device owners) have
a significant limitation: **they are not permanent**. On the "Device
administrators" page in the Settings app, you can revoke the permissions from
any device administrator app, which also allows you to uninstall the app. To a
user, that means that the policies are required *as long as the app is
installed*, but the user is always free to opt out of both the app and the
policies.

All camera-disabling apps on the Play Store use the device administration API,
so all of these apps can have their permissions revoked.

## Device owner apps

Android 5.0 introduced the concept of **device owner apps** (see the
[Provisioning for Device Administration](https://source.android.com/devices/tech/admin/provision.html)
docs). A device owner app is a special type of app that is permanently installed
on the device and cannot have its device administration permissions revoked. Any
Android device can only have a single device owner app set. An app can give up
its status as a device owner, but that is the only way that an app can stop
being a device owner.

Device owner apps are intended for an enterprise setting where the Android
device is provisioned by an IT department before its first use, so trying to set
an app as a device owner on a normal consumer phone/tablet is tricky, but not
impossible.

There are multiple ways to set a device owner:

* For production purposes, the device owner can be initialized either through
  NFC or through an activation code, and this must be done as the very first
  step when setting up the device. This approach requires that the device has
  *never* had an account set.
* For development purposes, the `dpm set-device-owner` command can be used to
  set an app as the device owner. This approach requires that the device
  *currently* have no accounts and have no secondary users.

Since the production approach only works on devices that have never been used,
the setup instructions use the development approach.

## Disabling the camera

Disabling the camera is done using the
[setCameraDisabled](http://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setCameraDisabled(android.content.ComponentName, boolean))
method, which instructs the Android system to disable all cameras. When any app
uses an API to access the camera, an exception will be thrown. Well-written apps
can handle this case and either display an error message or degrade gracefully,
although some apps may crash when attempting to use the camera.

## How Permanently Disable Camera works

The app itself is simple: it requests to be a device administrator, then allows
the user to disable the camera. It also detects whether it is a device owner to
know which message to display, but the app has no way to make itself a device
owner. The app does not, and will not, have any code for re-enabling the camera
or clearing its status as device owner.

Since the app cannot set itself as a device owner, this website provides
instructions for how to do so using the `dpm set-device-owner` approach with
ADB.

You can check out the
[source code on GitHub](https://github.com/disablecamera/disablecamera).
In particular, the
[DisableCameraActivity](https://github.com/disablecamera/disablecamera/blob/master/app/src/main/java/com/disablecamera/DisableCameraActivity.java)
class has all interesting implementation details.