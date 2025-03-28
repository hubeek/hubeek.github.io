# versions & beyond compare

_Status: Published_
_Created: 2018-10-03 02:33:28_
_Tags: macOS_

/Users/hjhubeek/Library/Application Support/Versions/Compare Scripts

on run argv
	set original_path to (item 1 of argv)
	set modified_path to (item 3 of argv)
	do shell script "/usr/local/bin/bcomp \"" & original_path & "\" \"" & modified_path & "\""
end run

in contents/resources of the Versions.app

in compareTools.plist
add to array of applications
<code>
<dict>
		<key>Name</key>
		<string>Beyond Compare</string>
		<key>Type</key>
		<string>ApplicationBinary</string>
		<key>Path</key>
		<string>BCompare.sh</string>
		<key>Application</key>
		<string>Beyond Compare</string>
	</dict>
</code>
create file Compare.sh
<code>
#!/bin/bash

export PATH=/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/usr/X11/bin

FILEMERGE=`/usr/local/bin/bcomp`
if [ ! -e "$FILEMERGE" ]; then
	FILEMERGE=/usr/local/bin/bcomp
fi

if [ ! -e "$FILEMERGE" ]; then
	FILEMERGE=/usr/local/bin/bcomp
fi

if [ ! -e "$FILEMERGE" ]; then
	echo "The FileMerge tool opendiff could not be located. Please install Xcode Tools from the Apple Developer website." >&2
	exit 1
fi

if [ -n "$3" ]; then
	"$FILEMERGE" "$1" "$2" -merge "$3"
else
	"$FILEMERGE" "$1" "$2"
fi

# on run argv
#   set original_path to (item 1 of argv)
#   set modified_path to (item 3 of argv)
#   do shell script "/usr/local/bin/bcomp \"" & original_path & "\" \"" & modified_path & "\""
# end run
</code>
avoid errors
<code>
#!/bin/sh
IFS=
bcompare "$6" "$7" -title1="$3" -title2="$5" -readonly
case $? in
'0','1','2')
exit 0
;;
'11','13','14')
exit 1
;;
'12')
echo "Important error???"
exit $?
;;
'*')
exit $?
;;
esac

</code>