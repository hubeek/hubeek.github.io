# remove mongo

_Status: Published_
_Created: 2017-06-01 16:42:28_
_Tags: terminal_

<code>
# See if mongo is in the launch/startup list
launchctl list | grep mongo

# Remove mongodb from the launch/startup
launchctl remove homebrew.mxcl.mongodb

# Kill the mongod process just in case it's running
pkill -f mongod

# Now you can safely remove mongodb using Homebrew
brew uninstall mongodb
</code>