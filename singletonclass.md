# SingletonClass

_Status: Published_
_Created: 2014-10-31 10:48:21_
_Tags: swift_

<code>class SingletonClass {
    class var shared : SingletonClass {

        struct Static {
            static let instance : SingletonClass = SingletonClass()
        }

        return Static.instance
    }
}</code>

use:
<code>let instance = SingletonClass.shared</code>