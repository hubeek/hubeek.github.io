# Hide status bar

_Status: Published_
_Created: 2015-02-04 06:12:42_
_Tags: swift_

add no to "View controller-based status bar appearance" in info.plist

add following to VC
<code>
override func prefersStatusBarHidden() -> Bool {
        return true
    }
</code>