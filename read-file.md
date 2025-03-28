# Read file

_Status: Published_
_Created: 2017-04-06 04:24:26_
_Tags: swift_

file io swift 2.2
<code>

        let fileLocation = NSBundle.mainBundle().pathForResource("2311393", ofType: "xml")!
        let text : String
        do
        {
            text = try String(contentsOfFile: fileLocation)
        }
        catch
        {
            text = ""
        }
</code>