# moving/renaming xcode

_Status: Published_
_Created: 2016-09-17 06:52:49_
_Tags: swift_

from:
/Applications/Xcode.app
=>
/Applications/xcode/Xcode73.app



sudo xcode-select -switch /Applications/xcode/Xcode73.app/Contents/Developer

remove xcode plugins:
rm -rf ~/Library/Application\ Support/Developer/Shared/Xcode/Plug-ins/*