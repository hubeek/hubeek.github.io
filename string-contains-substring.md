# String contains substring

_Status: Published_
_Created: 2018-02-21 02:17:52_
_Tags: iOS swift_

<code>
extension String {
    func contains(find: String) -> Bool{
        return self.range(of: find) != nil
    }
    func containsIgnoringCase(find: String) -> Bool{
        return self.range(of: find, options: .caseInsensitive) != nil
    }
}
</code>