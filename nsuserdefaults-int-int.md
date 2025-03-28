# NSUserDefaults [Int:Int]

_Status: Published_
_Created: 2016-07-27 09:06:51_
_Tags: swift_

<h2>load</h2>
<code>
if let data = NSUserDefaults.standardUserDefaults().objectForKey( "averagesPerLevel") as? NSData
{
    let object = NSKeyedUnarchiver.unarchiveObjectWithData(data) as! [Int: Int]
    print("average cached : \(object))")
}
</code>
<h2>save</h2>
<code>
NSUserDefaults.standardUserDefaults().setObject(NSKeyedArchiver.archivedDataWithRootObject(self.globalAverages!.averagesPerLevel), forKey:"averagesPerLevel")
</code>
