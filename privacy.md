---
layout: page
title: Privacy Policy - Permanently Disable Camera
permalink: /privacy/index.html
---

# Privacy Policy

Last modified: June 6, 2017.

This privacy policy describes the privacy practices of the Permanently Disable
Camera app for Android and explains the Android permissions used by the app.

## Use of the BIND_DEVICE_ADMIN Android permission

After installing, the app asks for the Android `BIND_DEVICE_ADMIN` permission.
This permission is used in two ways:

* When the app is installed, it uses the `setCameraDisabled` function to disable
  all cameras on the user's device. This is the primary purpose of the app.
* When the app is set as a Device Owner, it sets two policies:
  `DISALLOW_ADD_USER`, which prevents the user from adding additional device
  users, and `DISALLOW_FACTORY_RESET`, which prevents the user from performing
  a factory reset through the settings. Both of these policies are necessary to
  prevent the user from re-enabling the camera.

Before setting the app as a Device Owner, you may revoke the `BIND_DEVICE_ADMIN`
permission on the Device Administration Settings screen in the Android
preferences, which will re-enable all cameras. If you follow the instructions to
set the app as a Device Owner, you give up the ability to revoke the
`BIND_DEVICE_ADMIN` permission.

## No personal information collected

The app does not collect any personal information. It does not access the
internet, so it has no way of collecting information of any kind.

## Changes to this privacy policy

We reserve the right to make changes to this privacy policy at any time. Changes
will be published to this page, so we encourage you to check this page to
understand our current privacy practices.

## Contacting Us

If you have any questions regarding this privacy policy, you may contact the
developer at the email address
[disablecameradeveloper@gmail.com](mailto:disablecameradeveloper@gmail.com).