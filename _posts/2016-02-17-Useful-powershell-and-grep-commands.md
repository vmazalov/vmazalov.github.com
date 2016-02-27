---
layout: post
category : 
tagline: ""
tags : [Powershell, Commands]
---
{% include JB/setup %}

Some usefull Windows powershell and grep commands

* Select unique single letter words from a text file.

        cat textFile.txt |% { $_ -split '\s' } |? { $_ -match '^.$' } | select -Unique

* Select strings that contain a single characters surrounded by space and folloed by a number, e.g. " a -0.23243"

         sls '\s\w($|\s+-?[0-9.]+)' textFile.txt
         
* Find strings that contain capital letters

        cat list | grep -E \w*[A-Z]+\w*
        
* Find all strings in FileA which are not present in FileB

        grep -F -x -v -f fileB fileA
        
* Count lines in a file

        cat list | find /v /c ""
         
         
