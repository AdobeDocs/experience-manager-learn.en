---
title: AMS Dispatcher Basic File Layout
description: Understand the basic Apache and Dispatcher file layout.
version: 6.5
topic: Administration, Development
feature: Dispatcher
role: Admin
level: Beginner
thumbnail: xx.jpg
doc-type: Article
exl-id: 8a3f2bb9-3895-45c6-8bb5-15a6d2aac50e
duration: 354
---
# Basic File Layout

[Table of Contents](./overview.md)

[<- Previous: What is "The Dispatcher"](./what-is-the-dispatcher.md)

This document explains the AMS standard configuration file set and the thinking behind this configuration standard

## Default Enterprise Linux folder structure

In AMS the base installation uses Enterprise Linux as the base operating system. When installing Apache Webserver, it has a default install file set. Here are the default files that get installed by installing the basic RPM's provided by the yum repository

```
/etc/httpd/ 
├── conf 
│   ├── httpd.conf 
│   └── magic 
├── conf.d 
│   ├── autoindex.conf 
│   ├── README 
│   ├── userdir.conf 
│   └── welcome.conf 
├── conf.modules.d 
│   ├── 00-base.conf 
│   ├── 00-dav.conf 
│   ├── 00-lua.conf 
│   ├── 00-mpm.conf 
│   ├── 00-proxy.conf 
│   ├── 00-systemd.conf 
│   └── 01-cgi.conf 
├── logs -> ../../var/log/httpd 
├── modules -> ../../usr/lib64/httpd/modules 
└── run -> /run/httpd
```

When following and honoring the installation design / structure we gain the following benefits:

- Easier to support a predictable layout
- Automatically familiar to anyone who has worked on Enterprise Linux HTTPD installs in the past
- Allows patching cycles that are fully supported by the Operating System without any conflicts or manual adjustments
- Avoids SELinux violations of mislabeled file contexts

>[!BEGINSHADEBOX "Note"]

The Adobe Managed Services servers images typically have small Operating System root drives.  We put our data in a separate volume which is typically mounted in `/mnt` 
Then we use that volume instead of the defaults for the following default directories

`DocumentRoot`
- Default:`/var/www/html`
- AMS:`/mnt/var/www/html`

`Log Directory`
- Default: `/var/log/httpd`
- AMS: `/mnt/var/log/httpd`

Keep in mind that the old and new directories are mapped back to the original mount point to eliminate confusion.
Using a separate volume isn't vital but it's note worthy

>[!ENDSHADEBOX]

## AMS Add-ons

AMS adds on to the base install of Apache Web Server.

### Document Roots

AMS Default document roots:
- Author:
   - `/mnt/var/www/author/`
- Publish:
   - `/mnt/var/www/html/`
- Catch-All and Health Check Maintenance
   - `/mnt/var/www/default/`

### Staging and Enabled VirtualHost Directories

The following directories allow you to build out configuration files having a staging area that you can work on files and only enable then when they are ready.
- `/etc/httpd/conf.d/available_vhosts/`
   - This folder hosts all of your VirtualHost / files called `.vhost`
- `/etc/httpd/conf.d/enabled_vhosts/`
   - When you're ready to use the `.vhost` files, you have inside the `available_vhosts` folder symlink them using a relative path into the `enabled_vhosts` directory

### Additional `conf.d` Directories

There are additional pieces that are common in Apache configurations and we created sub directories to allow for a clean way to separate those files and not have all the files in one directory

#### Rewrites Directory

This directory can contain all of the `_rewrite.rules` files you create that contain your typical RewriteRulesyntax that engage Apache web servers [mod_rewrite](https://httpd.apache.org/docs/current/mod/mod_rewrite.html) module

- `/etc/httpd/conf.d/rewrites/`

#### Whitelists Directory

This directory can contain all of the `_whitelist.rules` files you create that contain your typical `IP Allow` or `Require IP`syntax that engage Apache web servers [access controls](https://httpd.apache.org/docs/2.4/howto/access.html)

- `/etc/httpd/conf.d/whitelists/`

#### Variables Directory

This directory can contain all of the `.vars` files you create that contain variables you can consume in your configuration files

- `/etc/httpd/conf.d/variables/`

### Dispatcher Module-specific Configuration Directory

Apache Web Server is very extensible and when a module has a lot of configuration files it's best practice to create your own configuration directory under the install base directory instead of cluttering up the default one.

We follow the best practice and created our own

#### Module Configuration file directory

- `/etc/httpd/conf.dispatcher.d/`

#### Staging and Enabled Farm

The following directories allow you to build out configuration files having a staging area that you can work on files and only enable then when they are ready.
- `/etc/httpd/conf.dispatcher.d/available_farms/`
   - This folder hosts all of your `/myfarm {` files called `_farm.any`
- `/etc/httpd/conf.dispatcher.d/enabled_farms/`
   - When you're ready to use the farm file, you have inside the available_farms folder symlink them using a relative path into the enabled_farms directory

### Additional `conf.dispatcher.d` Directories

There are additional pieces that are sub sections of the Dispatcher farm file configurations and we created sub directories to allow for a clean way to separate those files and not have a all the files in one directory

#### Cache Directory

This directory contains all of the `_cache.any`, `_invalidate.any` files you create that contain your rules on how you want the module to handle caching elements that come from AEM as well as invalidation rules syntax.  More details on this section are here [here](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache)

- `/etc/httpd/conf.dispatcher.d/cache/`

#### Client Headers Directory

This directory can contain all of the `_clientheaders.any` files you create that contain lists of Client Headers you want to pass through to AEM when a request comes in.  More details on this section are [here](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en)

- `/etc/httpd/conf.dispatcher.d/clientheaders/`

#### Filters Directory

This directory can contain all of the `_filters.any` files you create that contain all of your filter rules to block or allow traffic through the Dispatcher to reach AEM

- `/etc/httpd/conf.dispatcher.d/filters/`

#### Renders Directory

This directory can contain all of the `_renders.any` files you create that contain the connectivity details to each backend server that the dispatcher will consume content from

- `/etc/httpd/conf.dispatcher.d/renders/`

#### Vhosts Directory

This directory can contain all of the `_vhosts.any` files you create that contain a list of the domain names and paths to match to a particular farm to a particular back-end server

- `/etc/httpd/conf.dispatcher.d/vhosts/`

## Complete Folder Structure

AMS has structured each of the files with custom file extensions and with the intention to avoid namespace issues / conflicts and any confusion.

Here is an example of a standard fileset from an AMS default deployment:

```
/etc/httpd/
├── conf
│   ├── httpd.conf
│   └── magic
├── conf.d
│   ├── 000_init_ootb_vars.conf
│   ├── 001_init_ams_vars.conf
│   ├── README
│   ├── autoindex.conf
│   ├── available_vhosts
│   │   ├── 000_unhealthy_author.vhost
│   │   ├── 000_unhealthy_publish.vhost
│   │   ├── aem_author.vhost
│   │   ├── aem_flush.vhost
│   │   ├── aem_flush_author.vhost
│   │   ├── aem_health.vhost
│   │   ├── aem_publish.vhost
│   │   └── ams_lc.vhost
│   ├── dispatcher_vhost.conf
│   ├── enabled_vhosts
│   │   ├── aem_author.vhost -> ../available_vhosts/aem_author.vhost
│   │   ├── aem_flush.vhost -> ../available_vhosts/aem_flush.vhost
│   │   ├── aem_health.vhost -> /etc/httpd/conf.d/available_vhosts/aem_health.vhost
│   │   └── aem_publish.vhost -> ../available_vhosts/aem_publish.vhost
│   ├── logformat.conf
│   ├── mimetypes3d.conf
│   ├── remoteip.conf
│   ├── rewrites
│   │   ├── base_rewrite.rules
│   │   └── xforwarded_forcessl_rewrite.rules
│   ├── security.conf
│   ├── userdir.conf
│   ├── variables
│   │   ├── ams_default.vars
│   │   └── ootb.vars
│   ├── welcome.conf
│   └── whitelists
│       └── 000_base_whitelist.rules
├── conf.dispatcher.d
│   ├── available_farms
│   │   ├── 000_ams_catchall_farm.any
│   │   ├── 001_ams_author_flush_farm.any
│   │   ├── 001_ams_publish_flush_farm.any
│   │   ├── 002_ams_author_farm.any
│   │   ├── 002_ams_lc_farm.any
│   │   └── 002_ams_publish_farm.any
│   ├── cache
│   │   ├── ams_author_cache.any
│   │   ├── ams_author_invalidate_allowed.any
│   │   ├── ams_publish_cache.any
│   │   └── ams_publish_invalidate_allowed.any
│   ├── clientheaders
│   │   ├── ams_author_clientheaders.any
│   │   ├── ams_common_clientheaders.any
│   │   ├── ams_lc_clientheaders.any
│   │   └── ams_publish_clientheaders.any
│   ├── dispatcher.any
│   ├── enabled_farms
│   │   ├── 000_ams_catchall_farm.any -> ../available_farms/000_ams_catchall_farm.any
│   │   ├── 001_ams_author_flush_farm.any -> ../available_farms/001_ams_author_flush_farm.any
│   │   ├── 001_ams_publish_flush_farm.any -> ../available_farms/001_ams_publish_flush_farm.any
│   │   ├── 002_ams_author_farm.any -> ../available_farms/002_ams_author_farm.any
│   │   └── 002_ams_publish_farm.any -> ../available_farms/002_ams_publish_farm.any
│   ├── filters
│   │   ├── ams_author_filters.any
│   │   ├── ams_lc_filters.any
│   │   └── ams_publish_filters.any
│   ├── renders
│   │   ├── ams_author_renders.any
│   │   ├── ams_lc_renders.any
│   │   └── ams_publish_renders.any
│   └── vhosts
│       ├── ams_author_vhosts.any
│       ├── ams_lc_vhosts.any
│       └── ams_publish_vhosts.any
├── conf.modules.d
│   ├── 00-base.conf
│   ├── 00-dav.conf
│   ├── 00-lua.conf
│   ├── 00-mpm.conf
│   ├── 00-mpm.conf.old
│   ├── 00-proxy.conf
│   ├── 00-systemd.conf
│   ├── 01-cgi.conf
│   └── 02-dispatcher.conf
├── logs -> ../../var/log/httpd
├── modules -> ../../usr/lib64/httpd/modules
└── run -> /run/httpd
```

## Keeping it ideal

Enterprise Linux has patching cycles for the Apache Webserver Package (httpd).

The less installed default files you change the better, for reasons that if there is any patched security fixes or configuration improvements are applied via the RPM / Yum command it will not apply the fixes over the top of an altered file.

Instead it creates an `.rpmnew` file next to the original.  This means you'll miss some changes you might have wanted and created more garbage in your configuration folders.

i.e. The RPM during update installation will look at `httpd.conf` if it's in the `unaltered` state it will *replace* the file and you'll get the vital updates.  If the `httpd.conf` was `altered` then it *won't replace* the file and instead it will create a reference file called `httpd.conf.rpmnew` and the many desired fixes will be in that file that doesn't apply on service start-up.

Enterprise Linux was set up properly to handle this use case in a better way.  They give you areas in which you can extend or override the defaults they set for you.  Inside the base installation of httpd you'll find the file `/etc/httpd/conf/httpd.conf`, and it has syntax in it like:

```
Include conf.modules.d/.conf
IncludeOptional conf.d/.conf
```

The idea is that Apache wants you to extend the modules and configurations in adding new files to the `/etc/httpd/conf.d/` and `/etc/httpd/conf.modules.d/` directories with a file extension of `.conf`

As the perfect example when adding the Dispatcher module to Apache you'd create a module `.so` file in ` /etc/httpd/modules/` and then include it by adding a file in `/etc/httpd/conf.modules.d/02-dispatcher.conf` with the contents to load your module `.so` file

```
LoadModule dispatcher_module modules/mod_dispatcher.so
```

>[!NOTE]
>
>We didn't modify any already-existing files Apache provided. Instead, we just added ours to the directories they were meant to go.

Now we consume our module in our file <b>`/etc/httpd/conf.d/dispatcher_vhost.conf`</b> which initializes our module and loads the initial module-specific configuration file

```
<IfModule disp_apache2.c> 
    DispatcherConfig conf.dispatcher.d/dispatcher.any 
    ...SNIP... 
</IfModule>
```

Again you'll notice we've added files and modules but not altered any original files.  This gives us the desired functionality and protects us from missing wanted patch fixes as well as keeping to the highest level of compatibility with each upgrade of the package.

[Next -> Explanation of Configuration Files](./explanation-config-files.md)
