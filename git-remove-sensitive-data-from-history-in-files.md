# git remove sensitive data from history in files

_Status: Published_
_Created: 2019-08-26 15:25:47_
_Tags: git, cli_

<code>
git filter-branch --index-filter "git rm -rf --cached --ignore-unmatch path_to_file" HEAD
</code>
It’s a time intensive task might takes good amount of time to complete. As it has to check each commit and remove.
If you want to push it to remote repo just do git push
<code>
git push -all
</code>