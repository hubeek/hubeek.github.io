# meteor

_Status: Published_
_Created: 2017-02-19 02:10:17_
_Tags: raspberry pi_

<b>Install</b>
cd $HOME

git clone --depth 1 https://github.com/4commerce-technologies-AG/meteor.git

#now it installs if it is the first time!
$HOME/meteor/meteor --version

==========================
======= slow version     =======
==========================


cd $HOME

git clone --depth 1 https://github.com/4commerce-technologies-AG/meteor.git

cd meteor

Build bundled node:

scripts/build-node-for-dev-bundle.sh


Get mongodb installation from OS (e.g. Debian based):

sudo apt-get install mongodb


Optional (long runner) build bundled mongo:

scripts/build-node-for-dev-bundle.sh
Beneath the compiler and development tools and standard libaries, you have to also install the zlib1g-dev (or whatever it's named on your OS) library sources. Otherwise the mongo build will fail with an error like "-lz is missing"


Build meteor dev_bundle:

scripts/generate-dev-bundle.sh


Check installed version:

$HOME/meteor/meteor --version</code>
==========================
========= helpfull snips    =====
==========================

cd $HOME

# get the command line to checkout the meteor example
$HOME/meteor/meteor create --example simple-todos-react

# this is what you will receive as command hint, so put it in
git clone https://github.com/meteor/simple-todos-react

# jump into the project folder
cd simple-todos-react

# get necessary npm stuff
$HOME/meteor/meteor npm install

# bring that project up to latest module updates
$HOME/meteor/meteor update --packages-only

# add one package to avoid counting of modules usage and DDP error message on start
$HOME/meteor/meteor add package-stats-opt-out

# run that app
$HOME/meteor/meteor