---
comments: true
date: 2012-08-09 16:41:37
layout: post
slug: how-to-extract-text-from-ms-word-docs-in-linux
title: How to extract text from MS Word docs in linux
wordpress_id: 38
categories:
- exocortex
tags:
- .doc
- .docx
- bash
- linux
- text
---

For .doc: use antiword: linux utility that extracts texts from .doc files.

For .docx: extract text from ms word .docx files:

```bash
unzip -p some.docx word/document.xml | sed -e 's/<[^>]\{1,\}>//g; s/[^[:print:]]\{1,\}//g'
```

