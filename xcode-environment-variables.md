# xcode environment variables

_Status: Published_
_Created: 2018-05-25 04:46:18_
_Tags: iOS xcode_

<code>
if ProcessInfo.processInfo.environment["TESTING"] == "1"
{
    Constants.requestTimeoutInterval = 5
}
</code>