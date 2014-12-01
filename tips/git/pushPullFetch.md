# Push/Pull/Fetch
### Normal

    git push (-u) origin [local_source_branch]:[remote_destination_branch]
    git pull (-u) origin [remote_source_branch]:[local_destination_branch]
    git fetch (-u) origin [remote_source_branch]:[local_destination_branch]

```-u``` means setting default upstream, and is the abbreviation of ```--set-upstream```.

### Delete remote branch

    git push origin :[remote_destination_branch]

Push an empty branch to a remote branch means to delete the remote branch.
