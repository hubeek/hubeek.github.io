# bitbucket push origin problem

_Status: Published_
_Created: 2017-09-04 05:53:34_
_Tags: terminal git remote cli bash_

With Bitbucket problem on the raspi : 
```
git push -u origin master 
```
Counting objects: 87, done. 
error: pack-objects died of signal 9 
fatal: The remote end hung up unexpectedly 
fatal: The remote end hung up unexpectedly 
../html# fatal: write error: Bad file descriptor 
```
git config pack.windowMemory 10m
git config pack.packSizeLimit 20m
```

## Failed to push

in git: error: failed to push some refs to 

1. Insufficient permissions: You may not have the necessary permissions to push to the remote repository. Make sure you have the appropriate access rights and try again. Contact the repository owner or administrator if needed.
2. Network or connectivity issues: There might be network problems or connectivity issues preventing the push operation. Check your internet connection and try again. If the problem persists, it could be a temporary issue with the remote server or the network infrastructure.
3. Outdated local branch: If the remote repository has been updated since your last pull or clone, you might need to fetch and merge the changes before pushing your local changes. Use the git pull command to update your local branch and resolve any conflicts if necessary. Then attempt the push again.
4. Remote repository changes: It's possible that someone else has made changes to the remote repository, which conflict with your local changes. In this case, you need to pull the latest changes, resolve any conflicts, and then push your changes.
5. Git configuration issues: Verify your Git configuration settings, including your username and email address, to ensure they are correctly set up. Use the following commands to check and update if necessary: 
```
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```
6. Repository or branch restrictions: The remote repository may have certain restrictions in place, such as branch protection rules or branch permissions. Make sure you are following the guidelines and restrictions set by the repository.
