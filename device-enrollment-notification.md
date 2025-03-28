# Device Enrollment notification

_Status: Published_
_Created: 2018-04-03 02:21:49_
_Tags: OSX_

move
<code>
/System/Library/LaunchAgents/com.apple.ManagedClientAgent.enrollagent.plist
/System/Library/LaunchDaemons/com.apple.ManagedClient.enroll.plist
</code>
to
<code>
/Library/LaunchAgentsDisabled and /Library/LaunchDaemonsDisabled
</code>