---
layout: post
category : 
tagline: ""
tags : [Git, Git-LFS, Installation]
---
{% include JB/setup %}

This written primarily for Windows, but the same should apply to other platforms.

* Download and install (Git-LFS)[https://git-lfs.github.com/]
* If you have GitBash window open, you would have to reopen it.
* Run 

        git lfs install
        
* Configure the file share with

        git config --add lfs.url \\\\hostname\\fileshare\\path

* Make LFS track all dll files recursively  
        
        git lfs track "private/**/*.dll"
