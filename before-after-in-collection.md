# Before After in collection

_Status: Published_
_Created: 2016-12-14 17:42:23_
_Tags: swift_

<code>
public extension Collection where Iterator.Element: Equatable {
	
	public func after(_ element: Iterator.Element) -> Iterator.Element? {
		guard let idx = index(of: element), index(after: idx) < endIndex else { return nil }
		let nextIdx = index(after: idx)
		return self[nextIdx]
	}
	
	public func before(_ element: Iterator.Element) -> Iterator.Element? {
		guard let idx = index(of: element), index(before: idx) >= startIndex else { return nil }
		let previousIdx = index(idx, offsetBy: -1)
		return self[previousIdx]
	}
	
	public func index(before idx: Index) -> Index {
		return index(idx, offsetBy: -1)
	}
}
</code>