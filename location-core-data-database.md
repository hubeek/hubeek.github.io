# location core data database

_Status: Published_
_Created: 2015-03-18 08:33:37_
_Tags: swift_

<code>
func applicationDirectoryPath() -> String {
    return NSSearchPathForDirectoriesInDomains(.DocumentDirectory, .UserDomainMask, true).last! as String
}
</code>