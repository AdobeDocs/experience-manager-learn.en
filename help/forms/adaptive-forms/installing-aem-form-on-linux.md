---
title: Installing AEM Forms on Linux
description: Learn how to install 32-bit libraries for AEM Forms to work on Linux installation.
feature: Adaptive Forms
type: Tutorial
version: 6.4, 6.5
topic: Development
role: Developer
level: Beginner
jira: KT-7593
exl-id: b9809561-e9bd-4c67-bc18-5cab3e4aa138
last-substantial-update: 2019-06-09
duration: 216
---
# Installing 32 bit version of shared libraries

When AEM FORMS OSGi or AEM Forms j2EE is deployed on Linux, you have to ensure that 32-bit versions of a set of shared libraries are installed and available.  The descriptions are from the packages themselves. 

* expat (Stream-oriented XML parser C library for parsing XML, written by James Clark)
* fontconfig (Font configuration and customization library designed to locate fonts within the system and select them according to requirements specified by applications)
* freetype (Font rendering engine, developed to provide advanced font support for a variety of platforms and environments. It can open and manages font files as well as efficiently load, hint and render individual glyphs. It is not a font server or a complete text-rendering library)
* glibc (Core libraries for the GNU system and GNU/Linux systems, as well as many other systems that use Linux as the kernel)
* libcurl (Client-side URL transfer library)
* libICE (Inter-Client Exchange Library)
* libicu (Library that provides robust and full-featured Unicode and locale support - International Components for Unicode). Both 64-bit and 32-bit editions of this library is required
* libSM (X11 Session Management library)
* libuuid (DCE compatible Universally Unique Identifier library - used to generate unique identifiers for objects that may be accessible beyond the local system)
* libX11 (X11 client-side library)
* libXau (X11 Authorization Protocol - useful for restricting client access to the display)
* libxcb (X protocol C-language Binding - XCB)
* libXext (Library for common extensions to the X11 protocol)
* libXinerama (X11 extension which provides support for extending a desktop across multiple displays. The name is a pun on Cinerama, a widescreen movie format which used multiple projectors. libXinerama is the library which interfaces with the RandR extension)
* libXrandr (Xinerama extension is largely obsolete nowadays - it has been replaced by the RandR extension)
* libXrender (X Rendering Extension client library)
nss-softokn-freebl (Freebl library for Network Security Services)
* zlib (General-purpose, patent-free, lossless data compression library)

From Red Hat Enterprise Linux 6 onwards, the 32-bit edition of a library will have the filename extension .686 while the 64-bit edition will have .x86_64. Example, expat.i686. Prior to RHEL 6, 32-bit editions had the extension .i386. Before installing the 32-bit editions, make sure the latest 64-bit editions are installed. If the 64-bit edition of a library is older than the 32-bit version being installed, you will get an error such as below:

0mError: Protected multilib versions: libsepol-2.5-10.el7.x86_64 != libsepol-2.5-6.el7.i686 [0mError: Multilib version problems found.]

## First time install

On Red Hat Enterprise Linux, use the YellowDog Update Modifier (YUM) to install, as shown below:

1. yum install expat.i686
2. yum install fontconfig.i686
3. yum install freetype.i686
4. yum install glibc.i686
5. yum install libcurl.i686
6. yum install libICE.i686
7. yum install libicu.i686
8. yum install libicu
9. yum install libSM.i686
10. yum install libuuid.i686
11. yum install libX11.i686
12. yum install libXau.i686
13. yum install libxcb.i686
14. yum install libXext.i686
15. yum install libXinerama.i686
16. yum install libXrandr.i686
17. yum install libXrender.i686
18. yum install nss-softokn-freebl.i686
19. yum install zlib.i686

## Symlinks

Additionally, you need to create libcurl.so, libcrypto.so, and libssl.so symlinks pointing to the latest 32-bit versions of the libcurl, libcrypto, and libssl libraries respectively. You can find the files in /usr/lib/
ln -s /usr/lib/libcurl.so.4.5.0 /usr/lib/libcurl.so
ln -s /usr/lib/libcrypto.so.1.1.1c /usr/lib/libcrypto.so
ln -s /usr/lib/libssl.so.1.1.1c /usr/lib/libssl.so

## Updates to Existing System

here can be conflicts between the x86_64 and i686 architectures during updates, such as this:
Error: Transaction check error:
file /lib/ld-2.28.so from install of glibc-2.28-72.el8.i686 conflicts with file from package glibc32-2.28-42.1.el8.x86_64

If you run into this, un-install the offending package first, like in this case:
yum remove glibc32-2.28-42.1.el8.x86_64

All said and done, you want the x86_64 and i686 versions to be exactly the same, as for example from this output to the command:
yum info glibc

Last metadata expiration check: 0:41:33 ago on Sat 18 Jan 2020 11:37:08 AM EST.
Installed Packages
Name : glibc
Version : 2.28
Release : 72.el8
Architecture : i686
Size : 13 M
Source : glibc-2.28-72.el8.src.rpm
Repository : @System
From repo : BaseOS
Summary : The GNU libc libraries
URL : http://www.gnu.org/software/glibc/
License : LGPLv2+ and LGPLv2+ with exceptions and GPLv2+ and GPLv2+ with exceptions and BSD and Inner-Net and ISC and Public Domain and GFDL
Description : The glibc package contains standard libraries which are used by : multiple programs on the system. In order to save disk space and : memory, as well as to make upgrading easier, common system code is : kept in one place and shared between programs. This particular package : contains the most important sets of shared libraries: the standard C : library and the standard math library. Without these two libraries, a : Linux system will not function.

Name : glibc
Version : 2.28
Release : 72.el8
Architecture : x86_64
Size : 15 M
Source : glibc-2.28-72.el8.src.rpm
Repository : @System
From repo : BaseOS
Summary : The GNU libc libraries
URL : http://www.gnu.org/software/glibc/
License : LGPLv2+ and LGPLv2+ with exceptions and GPLv2+ and GPLv2+ with exceptions and BSD and Inner-Net and ISC and Public Domain and GFDL
Description : The glibc package contains standard libraries which are used by : multiple programs on the system. In order to save disk space and : memory, as well as to make upgrading easier, common system code is : kept in one place and shared between programs. This particular package : contains the most important sets of shared libraries: the standard C : library and the standard math library. Without these two libraries, a : Linux system will not function.

## Some useful yum commands

yum list installed
yum search [part_of_package_name]
yum whatprovides [package_name]
yum install [package_name]
yum reinstall [package_name]
yum info [package_name]
yum deplist [package_name]
yum remove [package_name]
yum check-update [package_name]
yum update [package_name]
