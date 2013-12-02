#Papertrail Charm



Overview
--------

This charm provides Papertrailapp logging from [Papertrail](http://www.papertrailapp.com). Papertrail provides instant log visibility. Use Papertrail's time-saving log tools, flexible system groups, team-wide access, long-term archives, charts and analytics exports, monitoring webhooks, and 45-second setup to ship your rsyslog logs, application output, and much more to Papertrail's logging service.

Usage
-----


    juju deploy papertrail
    juju set papertrail port=12345

##### IMPORTANT!

You must set the papertrail port for this charm to work. Papertrailapp provides a port once you've registered for service at http://www.papertrailapp.com. You can scrape this port from their installation configuration guide:

For RSyslog - it will appear as so:

	*.*          @logs.papertrailapp.com:1234


Configuration
-------------

- *int* port: Assigned syslog port from papertrail - *REQUIRED*

- *bool* monitorall: Monitor all logs in /var/log
- *string* applicationlogs: Space seperated list of application logs to monitor



Contact Information
-------------------

Author: Charles Butler (chuck@dasroot.net)

Report bugs at: http://bugs.launchpad.net/charms/+source/papertrail
Location: http://jujucharms.com/charms/precise/papertrail


