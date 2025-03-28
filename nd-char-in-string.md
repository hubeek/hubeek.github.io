# nd char in String

_Status: Published_
_Created: 2016-09-16 07:38:09_
_Tags: swift_

<code>
extension String {

    func index(at offset: Int, from start: Index? = nil) -> Index?
    {
        return index(start ?? startIndex, offsetBy: offset, limitedBy: endIndex)
    }

    func character(at offset: Int) -> Character?
    {
        precondition(offset >= 0, "offset can't be negative")
        guard let index = index(at: offset) else { return nil }
        return self[index]
    }

    subscript(_ range: CountableRange<Int>) -> Substring
    {
        precondition(range.lowerBound >= 0, "lowerBound can't be negative")
        let start = index(at: range.lowerBound) ?? endIndex
        return self[start..<(index(at: range.count, from: start) ?? endIndex)]
    }

    subscript(_ range: CountableClosedRange<Int>) -> Substring
    {
        precondition(range.lowerBound >= 0, "lowerBound can't be negative")
        let start = index(at: range.lowerBound) ?? endIndex
        return self[start..<(index(at: range.count, from: start) ?? endIndex)]
    }

    subscript(_ range: PartialRangeUpTo<Int>) -> Substring
    {
        return prefix(range.upperBound)
    }

    subscript(_ range: PartialRangeThrough<Int>) -> Substring
    {
        return prefix(range.upperBound+1)
    }

    subscript(_ range: PartialRangeFrom<Int>) -> Substring
    {
        return suffix(max(0, count-range.lowerBound))
    }

}

extension Substring {
    var string: String { return String(self) }
}
</code>
<code>
var abc = "abcdefg"
//2nd char
String(abc[abc.characters.startIndex.advancedBy(1)]) //"b"
</code>
get range with
<code>

extension String {
    
    subscript (i: Int) -> Character
    {
        return self[self.startIndex.advancedBy(i)]
    }
    
    subscript (r: Range<Int>) -> String
    {
        let start = startIndex.advancedBy(r.startIndex)
        let end = start.advancedBy(r.endIndex - r.startIndex)
        return self[Range(start ..< end)]
    }
}
</code>
results: abc[0...1] // "ab"
abc[1] = "a"
Or
<code>
Array(abc.characters)[1] //"b" 
</code>