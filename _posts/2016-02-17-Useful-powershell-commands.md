---
layout: post
category : 
tagline: ""
tags : [Powershell, Commands]
---
{% include JB/setup %}

Some usefull Windows powershell commands

* Select unique single letter words from a text file.

        cat textFile.txt |% { $_ -split '\s' } |? { $_ -match '^.$' } | select -Unique
