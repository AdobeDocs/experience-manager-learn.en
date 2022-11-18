---
title: Dispatcher Using and Understanding Variables
description: Understand how to use variables in your Apache and Dispatcher modules configuration files to take them to the next level.
version: Adobe Managed Service
topic: Administration, Configuration
feature: Dispatcher
role: Admin
level: Beginner
thumbnail: xx.jpg
---

# Using and Understanding Variables

[Table of Contents](./overview.html)

[<- Previous: Understanding Cache](./understanding-cache.md)

This document will explain how you can leverage the power of variables in Apache web server and in your dispatcher module configuration files.

## Variables

Apache supports variables and since version 4.1.9 of the Dispather module it supports them too!

We can leverage these to do a ton of useful things like:

- Make sure anything that is environment specific isn't inline in the configurations but extracted to make sure configuration files from dev work in prod with the same functional output.
- Toggle features and change log levels of immutable files AMS provides and won't let you change.
- Alter which includes to use based on variables like `RUNMODE` and `ENV_TYPE`
- Match `DocumentRoot`'s and `VirtualHost` DNS names between Apache configuraitons and module configurations.

## Using Baseline Variables

Due to the fact that AMS baseline files are read-only and immutable there are features that can be toggled off and on as well as being configured by editing the variables they consume.

### Baseline Variables

AMS default variables are declared in the file `/etc/httpd/conf.d/variables/ootb.vars`.  This file isn't editable but exists to make sure variables don't have null values.  They are included first then after than we include `/etc/httpd/conf.d/variables/ams_default.vars`.  You can edit that file to alter the values of these variables or even include the same variable names and values in your own file!

Here is a sample of the contents of the file `/etc/httpd/conf.d/variables/ams_default.vars`:

```
Define DISP_LOG_LEVEL info
Define AUTHOR_WHITELIST_ENABLED 0
Define PUBLISH_WHITELIST_ENABLED 0
Define AUTHOR_FORCE_SSL 1
Define PUBLISH_FORCE_SSL 0
```

### Example 1 - Force SSL

The variables shown above `AUHOR_FORCE_SSL`, or `PUBLISH_FORCE_SSL` can be set to 1 to enagage rewrite rules that force end users when coming in on http request to be redirected to https

Here is the configuration file syntax that allows this toggle to work:

```
</VirtualHost *:80> 
 <IfModule mod_rewrite.c> 
  ReWriteEngine on 
  <If "${PUBLISH_FORCE_SSL} == 1"> 
   Include /etc/httpd/conf.d/rewrites/forcessl_rewrite.rules 
  </If> 
 </IfModule> 
</VirtualHost>
```

As you can see the rewrite rules include is what has the code to redirect the end users browser, but the variable being set to 1 is what allows the file to be used or not

### Example 2 - Logging Level

The variables `DISP_LOG_LEVEL` can be used to set what you want to have for the log level that's actually used in the running configuration.

Here is the syntax example that exists in the ams baseline configuration files:

```
<IfModule disp_apache2.c> 
 DispatcherLog    logs/dispatcher.log  
 DispatcherLogLevel ${DISP_LOG_LEVEL} 
</IfModule>
```

If you need to increase the dispatcher logging level just update the `ams_default.vars` variable `DISP_LOG_LEVEL` to the level you'd like.

Example Values can be an integer or the word:

| Log Level | Integer Value | Word Value |
| --- | --- | --- |
| Trace | 4 | trace |
| Debug | 3 | debug |
| Info | 2 | info |
| Warning | 1 | warn |
| Error | 0 | error |

### Example 3 - Whitelists

The variables `AUTHOR_WHITELIST_ENABLED` and `PUBLISH_WHITELIST_ENABLED` can be set to 1 to engage rewrite rules that include rules to allow or disallow end user traffic based on IP address.  Toggling this feature on needs to be combined with creating a whitelist rules file as well for it to include.

Here is a few syntax examples of how the variable enables the includes of the whitelist files and a whitelist file example

`sample.vhost`:

```
<VirtualHost *:80> 
 <Directory /> 
  <If "${AUTHOR_WHITELIST_ENABLED} == 1"> 
   Include /etc/httpd/conf.d/whitelists/*_whitelist.rules 
  </If> 
 </Directory> 
</VirtualHost>
```

`sample_whitelist.rules`:

```
<RequireAny> 
  Require ip 10.43.0.10/24 
</RequireAny>
```

As you can see the `sample_whitelist.rules` enforces the IP restriction but toggling the variable allows it to be included in the `sample.vhost`

## Where to put the variables

### Web Server Start Up Arguments

AMS will put server / topology specific variables in the startup arguments of the Apache process inside the file `/etc/sysconfig/httpd`

This file has variables pre-defined like shown here:

```
AUTHOR_IP="10.43.0.59" 
AUTHOR_PORT="4502" 
AUTHOR_DOCROOT='/mnt/var/www/author' 
PUBLISH_IP="10.43.0.20" 
PUBLISH_PORT="4503" 
PUBLISH_DOCROOT='/mnt/var/www/html' 
ENV_TYPE='dev' 
RUNMODE='sites'
```

These aren't something you can change but are good to leverage in your configuration files

<div style="color: #000;border-left: 6px solid #2196F3;background-color:#ddffff;"><b>Note:</b>

Due to the fact that this file only gets included when the service starts up.  A restart of the service is required to pick up changes.  Meaning a reload isn't enough but a restart instead is needed
</div>

### Variables Files (`.vars`)

Custom variables provided by your code should live in `.vars` files inside the directory `/etc/httpd/conf.d/variables/`

These files can have any custom variables you'd like and some syntax examples can be seen in the following sample files

`/etc/httpd/conf.d/variables/weretail_domains_dev.vars`:

```
Define WERETAIL_DOMAIN dev.weretail.com 
Define WERETAIL_ALT_DOMAIN dev.weretail.net
```

`/etc/httpd/conf.d/variables/weretail_domains_stage.vars`:

```
Define WERETAIL_DOMAIN stage.weretail.com
Define WERETAIL_ALT_DOMAIN stage.weretail.net
```

`/etc/httpd/conf.d/variables/weretail_domains_prod.vars`:

```
Define WERETAIL_DOMAIN www.weretail.com 
Define WERETAIL_ALT_DOMAIN www..weretail.net
```

When creating your own variables files name them according to their content and to follow the naming standards provided in the manual [here](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17477.html#naming-convention).  In the above example you can see that the variables file hosts the different DNS entries as variables to use in the configuration files.

## Using Variables

Now that you've defined your variables inside your variables files you'll want to know how to use them properly inside your other configuration files.

We'll use the example `.vars` files from above to illustrate a proper use case.

We want to include all the environment based variables globally we'll create the file `/etc/httpd/conf.d/000_load_env_vars.conf`

```
IncludeOptional /etc/httpd/conf.d/variables/*_${ENV_TYPE}.vars
IncludeOptional /etc/httpd/conf.d/variables/*_${RUNMODE}.vars
```

We know that when the httpd service starts up it pulls in the variables set by AMS in `/etc/sysconfig/httpd` and has the variable set of `ENV_TYPE` and `RUNMODE`

When this global `.conf` file gets pulled in it will be pulled in early because the include order of files in `conf.d` is alpha numeric load order mean 000 in the filename will assure that it loads before the other files in the directory.

The include statement is also using a variable in the filename.  This can change which file it will actually loads based on what value is in the `ENV_TYPE` and `RUNMODE` variables.

If the `ENV_TYPE` value is `dev` then the file that gets used is:

`/etc/httpd/conf.d/variables/weretail_domains_dev.vars`

If the `ENV_TYPE` value is `stage` then the file that gets used is:

`/etc/httpd/conf.d/variables/weretail_domains_stage.vars`

If the `RUNMODE` value is `preview` then the file that gets used is:

`/etc/httpd/conf.d/variables/weretail_domains_preview.vars`

When that file gets included it will allow us to use the variable names that were stored inside.

In our `/etc/httpd/conf.d/available_vhosts/weretail.vhost` file we can swap out the normal syntax that only worked for dev:

```
<VirtualHost *:80> 
 ServerName dev.weretail.com 
 ServerAlias dev.weretail.net
```

With newer syntax that uses the power of variables to work for dev, stage, and prod:

```
<VirtualHost *:80> 
 ServerName ${WERETAIL_DOMAIN} 
 ServerAlias ${WERETAIL_ALT_DOMAIN}
```

In our `/etc/httpd/conf.dispatcher.d/vhosts/weretail_vhosts.any` file we can swap out the normal syntax that only worked for dev:

```
"dev.weretail.com" 
"dev.weretail.net"
```

With newer syntax that uses the power of variables to work for dev, stage, and prod:

```
"${WERETAIL_DOMAIN}" 
"${WERETAIL_ALT_DOMAIN}"
```

These variables have a huge amount of re-use to individualize running settings without having to have different deployed files per environment.  You essentially templatize your configuration files with the use of variables and include files based on variables.

## Viewing variable values

Sometimes when using variables we have to search to see what the values might be in our configuration files.  There is a way to view the resolved variables by running the following commands on the server:

```
source /etc/sysconfig/httpd;/sbin/httpd -S | grep Define | grep "="
```

How the variables looked in your compiled Apache configuration:

```
$ source /etc/sysconfig/httpd;/sbin/httpd -t -D DUMP_CONFIG | grep -v "#"
```

How the variables looked in your compiled Dispatcher configuration:

```
$ source /etc/sysconfig/httpd;/sbin/httpd -t -D DUMP_ANY
```

From the output of the commands you'll see the differences of the variable in the config file vs the compiled output.

Example Configuration

`/etc/httpd/conf.d/enabled_vhosts/aem_publish.vhost`:

```
<VirtualHost *:80> 
	DocumentRoot	${PUBLISH_DOCROOT} 
```

Now run the commands to see the compiled output

Compiled Apache Config:

```
$ source /etc/sysconfig/httpd;/sbin/httpd -t -D DUMP_CONFIG | grep DocumentRoot
DocumentRoot /mnt/var/www/html
```

Compiled Dispatcher Config:

```
$ source /etc/sysconfig/httpd;/sbin/httpd -t -D DUMP_ANY | grep docroot
/docroot "/mnt/var/www/html"
```

[Next -> Flushing](./disp-flushing.md)