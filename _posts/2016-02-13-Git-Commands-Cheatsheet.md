---
layout: post
category : 
tagline: ""
tags : [Git, Commands]
---
{% include JB/setup %}

I will be recording  here some of the commonly used Git commands:

* Init repo and clone (note that for windows locations, one should use file:////hostname/path/to/repo)

        Git init
	Git clone remote_repo_location

* Show refs

        git show-ref
	
* Add all modified files

        git add -A

* Revert to certain commit and push to remote

        git reset --hard <commit_id>
        git push -f
        
* Push the local branch to remote

        git push --set-upstream origin <branch_name>

* Manager tracked repositories

        git remote
   
* Checkout a branch from a remote

        git checkout -b < new_branch > origin/< new_branch >
	
* Some other common commands

        Git status
        git log
        Git cherry-pick <commit_id>
        git pull
        git rebase origin/master
        git push origin HEAD:branch_Name
  
