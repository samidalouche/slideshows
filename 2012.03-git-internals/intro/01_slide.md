!SLIDE 
# Git internals #

Sami Dalouche (<sami.dalouche@gmail.com>)

!SLIDE bullets incremental transition=scrollUp
# I assume you know... #

 * basic git usage (clone/push/pull/commit)
 * what distributed source control is 
 * that git is awesome 

!SLIDE bullets incremental transition=scrollUp
# Git is simple #

* Working Directory
* Objects
* Index
* Refs and Remotes

!SLIDE commandline incremental transition=scrollUp

# Git Directory #

    $>tree -L 1
    .
    |-- HEAD         # pointer to your current branch
    |-- config       # your configuration preferences
    |-- description  # description of your project 
    |-- hooks/       # pre/post action hooks
    |-- index        # index file (see next section)
    |-- logs/        # a history of where your branches have been
    |-- objects/     # your objects (commits, trees, blobs, tags)
    `-- refs/        # pointers to your branches

!SLIDE center transition=scrollUp

# Git Object Model (1/2) #

![octocat](../pictures/objects-example.png)

!SLIDE center transition=scrollUp

# Git Object Model (2/2) #

![tag](../pictures/object-tag.png)

!SLIDE commandline incremental transition=scrollUp

# Git Index #

    $>git status
    .
    On branch master
    Your branch is behind 'origin/master' by 11 commits, 
    and can be fast-forwarded.
    
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
   
      modified:   daemon.c
    
    Changed but not updated:
       (use "git add <file>..." to update what will be committed)
    
       modified:   grep.c
       modified:   grep.h
    
     Untracked files:
       (use "git add <file>..." to include in what will be committed)
   
       blametree
       blametree-init
       git-gui/git-citool

!SLIDE bullets incremental transition=scrollUp

# References and Remotes #

* Simple pointers to commits
* Simple files with commit ID 
* Remote pointers updated by pull/fetch

!SLIDE bullets incremental transition=scrollUp

# On Immutability #

* Git objects are Immutable
* Git objects are Immutable
* GC is sometimes needed

!SLIDE bullets incremental transition=scrollUp

# An example #

![rebase](../pictures/rebase0.png)

!SLIDE bullets incremental transition=scrollUp

# Let's do some work #

![rebase](../pictures/rebase1.png)

!SLIDE bullets incremental transition=scrollUp

# Merge #

![rebase](../pictures/rebase2.png)

!SLIDE bullets incremental transition=scrollUp

# Rebase (1/3) #

![rebase](../pictures/rebase3.png)

!SLIDE bullets incremental transition=scrollUp

# Rebase (2/3) #

![rebase](../pictures/rebase4.png)


!SLIDE bullets incremental transition=scrollUp

# Rebase (3/3) #

![rebase](../pictures/rebase5.png)

!SLIDE bullets incremental transition=scrollUp

# The rest is 'just' syntax #

* git rebase -i / git add -i
* git bissect
* git reflog
* git stash
* git reset/clean/checkout/revert

!SLIDE center transition=scrollUp

# Thank You !#
