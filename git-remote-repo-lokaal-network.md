# Git remote repo lokaal network

_Status: Published_
_Created: 2016-06-07 04:54:08_
_Tags: terminal git remote_

op de server git proj maken
<code>
mkdir repoName.git
cd repoName.git/
git --bare init
Initialized empty Git repository in /volume1/git/repoName.git/
git update-server-info
cd ..
chown -R loginname repoName.git 
</code>

clonen proj van server
<code>
git clone ssh://login@192.168.0.1/volume1/git/repoName.git
</code>

lokaal proj files toevoegen:
<code>
git init
git remote add origin ssh://login@192.168.0.1/volume1/git/repoName.git
//git push -f
git config --global push.default simple
// add your files
git add .
git commit -a -m "Initial Commit"
git push -u origin --all
</code>

extra:
<code>
git remote
bv : origin
</code>

<code>
git remote -v
origin	https://github.com/schacon/ticgit (fetch)
origin	https://github.com/schacon/ticgit (push)
</code>

push to remote
<code>
git push origin master
</code>

inspecting
<code>
git remote show origin
</code>

renaming
<code>
$ git remote rename pb paul
$ git remote
origin
paul
</code>

removing
<code>
$ git remote rm paul
$ git remote
origin
</code>