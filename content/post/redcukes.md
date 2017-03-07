+++
date = "2012-03-21T17:46:00+05:30"
draft = false
title = "Redcukes"
subtitle="Running redmine stories using cucumber"
description="Running redmine stories using cucumber"
keywords = ["ruby", "cucumber"]
categories = [ "Development","Ruby" ]
author = "Jijesh Mohan"
socialsharing = true
notoc = true
+++

I have seen projects where userstories are managed in redmine along with acceptance criteria. But while automating with cucumber all these stories and scenarios are again replicated in cucumber feature files. This leads to inconsistency due to the story modification in redmine which is not synced with cucumber feature files.

To avoid this problem I have developed a ruby gem called [Redcukes](https://github.com/jijeshmohan/redcukes) for integrating redmine with cucumber and we can run cucumber against the user stories stored in redmine and update execution status back to redmine.

For using this gem, make sure that the REST API is enabled in redmine (``Administration > Settings -> Authentication -> Enable REST web service``). It is better to define another user role for cucumber tests with required issue modification rights.

Install gem using gem install redcukes. In cucumber projects directory, create env.rb under support directory.

Edit env.rb file and add following configuration

```ruby
require 'redcukes'

Redcukes::Redmine.configure do |config|
 config.site = redmine url
 config.user = redmine username
 config.password = redmine password
 end
```

It is also possible to add issue filter using search_filter property

e.g : ```config.search_filter = {:project_id => ‘iframe’,:tracker_id => 2}```

The default status updates are “Resolved” or “Rejected” according to feature passed or failed. This can be customized like below

e.g ```config.result_status = {:passed => 7,:failed => 8}```


I have created two more issue status called Passed, Failed and gave given these status ids in the above configuration.

This will be a perfect executable documentation for your project.
