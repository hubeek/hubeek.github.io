# Elapsed Time

_Status: Published_
_Created: 2016-02-19 02:56:24_
_Tags: swift_

<code>
let start1 = NSDate()
//.. Do Something ..
let end1 = NSDate()
let timeInterval: Double = end1.timeIntervalSinceDate(start1)
print("Elapsed Time: \(timeInterval)")
</code>