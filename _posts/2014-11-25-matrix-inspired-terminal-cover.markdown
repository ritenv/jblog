---
layout: post
title:  Matrix-inspired Terminal Cover for OSX
date:   2014-11-26 00:27:25
categories: matrix terminal osx
image: /assets/article_images/2014-11-24-interactive-fiction/ifiction.jpg
---

## A Continous-Output Terminal

I particularly like this terminal snippet for how it gives an intense feeling. Make your OSX terminal look awesome.
Ensure to have your terminal themed with the built-in "Pro" theme for best results.

Simply paste the below script.


```
LC_ALL=C tr -c "[:digit:]" " " < /dev/urandom | dd cbs=$COLUMNS conv=unblock | GREP_COLOR="1;32" grep --color "[^ ]"
```