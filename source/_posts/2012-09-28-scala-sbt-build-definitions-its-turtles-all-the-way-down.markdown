---
comments: false
date: 2012-09-28 23:33:10
layout: post
slug: scala-sbt-build-definitions-its-turtles-all-the-way-down
title: 'Scala SBT build definitions: it''s turtles all the way down!'
wordpress_id: 348
categories:
- exocortex
tags:
- sbt
- scala
---

From: (https://github.com/harrah/xsbt/wiki/Getting-Started-Full-Def)

```bash
 hello/                  # your project's base directory

     Hello.scala         # a source file in your project (could be in
                         #   src/main/scala too)

     build.sbt           # build.sbt is part of the source code for the
                         #   build definition project inside project/

     project/            # base directory of the build definition project

         Build.scala     # a source file in the project/ project,
                         #   that is, a source file in the build definition

         build.sbt       # this is part of a build definition for a project
                         #   in project/project ; build definition's build
                         #   definition


         project/        # base directory of the build definition project
                         #   for the build definition

             Build.scala # source file in the project/project/ project
```
