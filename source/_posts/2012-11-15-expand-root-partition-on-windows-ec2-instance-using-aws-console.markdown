---
comments: false
date: 2012-11-15 09:28:21
layout: post
slug: expand-root-partition-on-windows-ec2-instance-using-aws-console
title: Expand root partition on Windows EC2 instance using AWS Console
wordpress_id: 404
categories:
- exocortex
tags:
- ec2
---

* Stop instance.
* Create AMI from instance, choosing to expand partition.
* Start instance and log in
* Control Panel -> Create and Format Disk Partitions
* Extend partition
