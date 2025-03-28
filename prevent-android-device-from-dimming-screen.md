# prevent android device from dimming screen

_Status: Published_
_Created: 2014-10-02 06:00:47_
_Tags: Actionscript_

in main.as
<code>NativeApplication.nativeApplication.systemIdleMode = SystemIdleMode.KEEP_AWAKE;</code>

in application.xml
<code><uses-permission android:name="android.permission.WAKE_LOCK"/> </code>