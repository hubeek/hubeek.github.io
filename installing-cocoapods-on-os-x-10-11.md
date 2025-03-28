# Installing CocoaPods on OS X 10.11

_Status: Published_
_Created: 2016-04-06 05:24:56_
_Tags: swift_

Installing CocoaPods on OS X 10.11

$ sudo chmod -R 755 /usr/local/bin
$ sudo gem uninstall cocoapods
Remove executables:
    pod, sandbox-pod

in addition to the gem? [Yn]  Y

$  gem install cocoa pods

$ pod install


==
OR
==

These instructions were tested on all betas and the final release of El Capitan.

Custom GEM_HOME

This is the solution when you are receiving Above Error

$ mkdir -p $HOME/Software/ruby
$ export GEM_HOME=$HOME/Software/ruby
$ gem install cocoapods
[...]
1 gem installed
$ export PATH=$PATH:$HOME/Software/ruby/bin
$ pod --version