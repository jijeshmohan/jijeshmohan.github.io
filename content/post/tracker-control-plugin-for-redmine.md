+++
date = "2011-12-24T17:46:00+05:30"
draft = false
title = "Tracker control plugin for redmine"
description="Tracker control plugin for redmine"
keywords = ["redmine", "tracker control","plugin"]
categories = [ "Development","Ruby" ]
author = "Jijesh Mohan"
socialsharing = true
notoc = true
+++

For the last couple of months I have started using redmine project management tool for my official work . The tool has most of the features including issue tracker, built-in wiki, forum and can even integrate SCM. Redmine is developed in ruby on rails platform and supports plug-ins which helps to add new features to the tool.

One of the feature which my team was looking at is to control the tracker wise issue creation, for example developers should not be able to create new requirement(tracker) issue. Redmine has access permission only in the issue creation level but not in tracker wise.

To add the above functionality to redmine, I have created a new redmine plugin called [Redmine Tracker Control](http://www.redmine.org/plugins/redmine_track_control). The plugin supports following **features**: 

* Role based permission for creating issue with specific Tracker
* Project Module to enable/disable tracker permission
* Projects which are not enabled for tracker control module, uses default redmine behavior

#### Installation

* Copy redmine_track_control directory to ``#{RAILS_ROOT}/vendor/plugins``
* Restart Redmine
* Goto ``Redmine -> Administration -> Roles and Permissions  -> Permissions report``
* Configure the permissions in Tracker Permissions section

{{< figure src="/img/track_control.jpg" >}}

To enable tracker permissions to project, Go to the ``project -> Settings -> Modules`` and enable Tracker Permissions Module

You can download plugin from [Github](https://github.com/jijeshmohan/redmine_track_control)
