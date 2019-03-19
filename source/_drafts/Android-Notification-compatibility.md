---
title: Android-Notification-compatibility
permalink: Android-Notification-compatibility
toc: false
date: 2019-03-19 13:38:52
tags:
categories:
---
Notification compatibility
Since Android 1.0, the notification system UI and the notification-related APIs have continually evolved. To use the latest notification API features while still supporting older devices, use the support library notification API:NotificationCompat and its subclasses, as well as NotificationManagerCompat. This will allow you to avoid writing conditional code to check API levels because these APIs handle that for you.
NotificationCompat is updated as the platform evolves to include the latest methods. It is important to note that the availability of a method in NotificationCompat does not guarantee that the corresponding feature will be provided on older devices. In some cases calling a newly-introduced API results in a no-op on older devices. For example,NotificationCompat.addAction() displays the action button on a device running Android 4.1 (API level 16) and higher only.
The following is a summary of the most notable behavior changes for Android notifications.
Android 4.1, API level 16
Introduced expandable notification templates (called notification styles), allowing for larger notification content area to display information. Users can use a one finger swipe up/down gesture to expand a notification.
Also introduced the ability to add additional actions, in the form of buttons, to a notification.
Added ability for users to turn notifications off on a per-app basis in settings.
Android 4.4, API level 19 and 20
Notification listener services were added to the API.
Android Wear (now called Wear OS) support was added in API level 20.
Android 5.0, API level 21
Introduced lock screen and heads-up notifications.
The user can now put the phone into Do Not Disturb mode and configure which notifications are allowed to interrupt them when the device is in priority only mode.
Methods added to API set whether or not a notification is displayed on the lock screen (setVisibility()) and for specifying “public” version of the notification text.
setPriority() method added which tells the system how “interruptive” this notification should be (e.g. setting it to high makes the notification appear as a heads-up notification).
Notification stacks support added to Android Wear (now called Wear OS) devices. Put notifications into a stack using setGroup(). Note that notification stacks were not supported on tablets nor phones yet. Notification stacks would later become known as a group or bundle.
Android 7.0, API level 24
Notification templates were restyled to put emphasis on the hero image and avatar.
Three notification templates were added: one for messaging apps and the other two for decorating custom content views with the expandable affordance and other system decorations.
Support added to handheld devices (phones and tablets) for notification groups. Uses the same API as Android Wear (now called Wear OS) notification stacks introduced in Android 5.0 (API level 21).
Users can reply directly inside of a notification (they can enter text which will then be routed to the notification’s parent app) using inline reply.
Android 8.0, API level 26
Individual notifications must now be put in a specific channel.
Users can now turn off notifications per channel, instead of turning off all notifications from an app.
Apps with active notifications display a notification "badge" on top of their app icon on the home/launcher screen.
Users can now snooze a notification from the drawer. You can set an automatic timeout for a notification.
You can also set the notification's background color.
Some APIs regarding notification behaviors were moved from Notification to NotificationChannel. For example, use NotificationChannel.setImportance() instead of NotificationCompat.Builder.setPriority() for Android 8.0 and higher.
