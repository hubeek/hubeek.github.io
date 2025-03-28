# SwiftUI small techniques

_Status: Published_
_Created: 2019-06-22 01:53:37_
_Tags: swift, swiftUI_

do after 1 seconds
<code>
@State var reloadCount = 0 
...
body
---
DispatchQueue.main.asyncAfter(deadline: .now() + 1) {
  self.reloadCount += 1
}
</code>

Bool
<code>
var isBoolean = false
...
isBoolean.toggle()
</code>