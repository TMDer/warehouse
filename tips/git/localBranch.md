# Local Branch
### Create branch and checkout that branch

    git checkout -b [new_branch_name]

### Track remote branch

    git branch -u [remote_branch_to_be_tracked] ([local_branch])
    
```-u``` means setting default upstream, and is the abbreviation of ```--set-upstream```.

Not specifying [local_branch] means the branch checkout now.

### Rename branch

    git branch -m ([branch_origin_name]) [branch_new_name]

Not specifying [branch_origin_name] means the branch checkout now.

### Delete branch

    git branch -D [local_branch]
