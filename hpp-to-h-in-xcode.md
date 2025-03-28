# hpp to .h in Xcode

_Status: Published_
_Created: 2015-12-05 03:26:31_
_Tags: OF_

The behavior can be changed quite easily by renaming the file ___FILEBASENAME___.hpp to ___FILEBASENAME___.h in this folder:

/Applications/Xcode.app/Contents/Developer/Library/Xcode/Templates/File\ Templates/Source/C++\ File.xctemplate/WithHeader
Also you have to change all occurences of "hpp" to "h" in both template files in this folder.