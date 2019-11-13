# Listribute v1

The first version of Listribute was created with Ionic (cordova based framework) and a PHP backend. It is still in use, though the app was removed from AppStore and Google Play due to lack of maintenance. This document is a description of how it was built and how it works.

## Architecture

Backend is a RESTful API written in PHP with [phpREST](https://github.com/veloek/php-rest). It handles authentication, CRUD operations on users, lists, subscriptions and items, in addition to sending push notifications. It is backed by a small MySQL database and runs on a hosted "web hotel" service.

The app is written with Ionic v1, an AngularJS based framework for building cross-platform mobile applications. It uses several plugins to access native functionality, like push notifications and camera etc.

In order to achive "realtime" updates from other people while using the app, push notifications are being sent from the server to tell the app to reload. Push notifications are not guaranteed to be delivered right away, but in most cases they are and that was good enough for this application.

## Functionality

The main functionality consist of user handling, creating lists and items and choosing how to share those lists with. There are some quirks though, and those are described in each of the subsections below.

### User handling

When the app is started the first time, a request is sent to the server to create a user. When it's created, the credentials are stored in local storage. This all happens in the background without the user noticing. Thus the first view presented is the "list of lists" aka home page.

In the app, there's a settings section where the user can change the predefined username and enter an email address. The email address is only used to receive the password. The password is only needed if the app is re-installed and you want to get your old lists back. You can then use the username and password to switch back to the previous user.

### Lists

List are created with a "+" button on the home page. The name is predefined to be current date and you're navigated to the list of items.

From the home page you're able to change settings for a given list by long-pressing the entry. The settings page consists of a name field, a field to add new subscribers and a list of subscribers for that list. Any subscriber of the list can edit the name and add new subscribers. Only the subscriber can unsubscribe.

### Items

Items can be added to a list by anyone who subscribes to that list. Any item can be deleted, checked off or have it's description edited by any of the subscribers, but it's prohibited to change the title (the idea was that if someone has already checked off the item, it shouldn't be possible to change what they have checked off).

An item can have a more detailed description and an image attached to it, which can be edited by long-pressing the entry.

## Summary

This project was a one-man show developed rather intensively throughout a summer in 2014. It was a struggle to get push notification working with both APN and GCM, but once it was working the app was behaving relatively well without the need for much maintenance. New certificates needed to be provisioned from time to time, but that was a rather quick and easy procedure. The state of the current app is that it's removed from the stores, push notifications no longer work and only a few users are still using it. The ones that used it was very happy with it though, so I think it deserves a revival!
