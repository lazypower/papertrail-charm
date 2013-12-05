# Papertrail
  
This charm provides Papertrailapp logging from [Papertrail](http://www.papertrailapp.com). Papertrail provides instant log visibility. Use Papertrail's time-saving log tools, flexible system groups, te  am-wide access, long-term archives, charts and analytics exports, monitoring webhooks, and 45-second setup to ship your rsyslog logs, application output, and much more to Papertrail's logging service.


##### IMPORTANT!

You must set the papertrail syslog endpoint for this charm to work. Papertrail provides this location once you've registered for service at [http://www.papertrailapp.com](http://www.papertrailapp.com).   You can collect the syslog endpoint from their installation configuration guide: [here](https://papertrailapp.com/systems/setup)


## Configuration

`syslog_endpoint` : Paste your provided papertrail syslog endpoint string exactly as shown. (ex: logs.papertrailapp.com:1234)


`monitorall` : If you want to monitor every file in /var/log and its subdirectories, enable this option. Default: False


`applicationlogs` : Space separated list of full paths to logs you would like to ship to papertrail.

ex: ` /opt/minecraft/server.log /home/deploy/deploy_output.txt`

## Usage

To use the papertrail charm, it is deployed to your Juju canvas as a subordinate unit. You can easily distinguish this type of charm from other charms by the presence of the squiggly indicator box.

Let's add Papertrail log aggregation to our Wordpress stack. 

Assuming you've bootstrapped your environment, deploy MySQL and the Wordpress charms.

```
$ juju deploy mysql
$ juju deploy wordpress
$ juju add-relation wordpress mysql
```
The above set of commands will deploy a wordpress stack, and configure the database relationship between them.

Now we are ready to deploy the papertrail charm

```
$ juju deploy papertrail
```

We'll need to set the papertrail provided endpoint

```
$ juju set papertrail syslog_endpoint=logs.papertrailapp.com:1234
```
and lets add the relationship to our application servers. By default this
will only ship syslog data.

```
$ juju add-relation papertrail wordpress
$ juju add-relation papertrail mysql

```

To add the webserver logs, we will need to add the fullpath to the log(s) we want to monitor

```
$ juju set papertrail applicationlogs="/mnt/access.log /mnt/error.log"

```

We are now shipping our HTTP Access, Error, and syslog's for both systems to papertrail's logging nexus. 

#### Note
The application logs configuration also supports wildcard notation. For example if /mnt/logs contains 3 files, foobar.svg output.log input.log - you can ship the two log files with the following configuration

```
$ juju set papertrail applicationlogs="/mnt/logs/*.log"
```



## Caveats

#### Syslog Daemons
This charm has only been tested on Ubuntu 12.04 LTS + and makes the following assumptions:

You are using rsyslog, the default syslog package in ubuntu 12.04 LTS, or you are using syslog-ng. 

If you wish to monitor an older system d style syslog daemon, you will need to manually set the log files to watch with the applicationlog configuration variable. 

#### Use of Ruby for Application Logs

At present, the remote_syslog gem is used to watch application logs, and the monitorall flag consumes the remote_syslog gem. If this violates your belief in using only packages from the Ubuntu Archive and not third party gems: this may pose a problem for you.


 

## Contact Information

  Author: Charles Butler (chuck@dasroot.net)

  Report bugs at: http://bugs.launchpad.net/charms/+source/papertrail
  Location: http://jujucharms.com/charms/precise/papertrail
  
## Licensing
  This charm is Creative Commons Share Alike 4.0 Licensed
