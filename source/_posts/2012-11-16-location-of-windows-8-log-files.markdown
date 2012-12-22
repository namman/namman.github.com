---
comments: false
date: 2012-11-16 10:38:14
layout: post
slug: location-of-windows-8-log-files
title: Location of Windows 8 log files
wordpress_id: 409
categories:
- exocortex
tags:
- logs
- windows 8
---

$windows.~bt\Sources\Panther: Log location before Setup can access the drive.
$windows.~bt\Sources\Rollback: Log location when Setup rolls back in the event of a fatal error.
%WINDIR%\Panther: Log location of Setup actions after disk configuration.
%WINDIR%\Inf\Setupapi*.log: Used to log Plug and Play device installations.
%WINDIR%\Memory.dmp: Location of memory dump from bug checks.
%WINDIR%\Minidump\*.dmp: Location of log minidumps from bug checks.
%WINDIR%\System32\Sysprep\Panther: Location of Sysprep logs.
%WINDIR%\System32\LogFiles\Srt\SrtTrail.txt: Startup repair log.
