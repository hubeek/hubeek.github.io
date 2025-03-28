# Regex

_Status: Published_
_Created: 2016-10-15 02:04:05_
_Tags: swift_

<code>
func matchesForRegexInText(regex: String, text: String) -> [String] {

    do {
        let regex = try NSRegularExpression(pattern: regex, options: [])
        let nsString = text as NSString
        let results = regex.matchesInString(text,
                                            options: [], range: NSMakeRange(0, nsString.length))
        return results.map { nsString.substringWithRange($0.range)}
    } catch let error as NSError {
        print("invalid regex: \(error.localizedDescription)")
        return []
    }
}

var string = "aarde"
matchesForRegexInText("aa..e", text: string)
</code>