# base64

_Status: Published_
_Created: 2016-10-27 02:46:49_
_Tags: swift_

<code>
var str = "Hello, playground"
let utf8str = str.dataUsingEncoding(NSUTF8StringEncoding)//<48656c6c 6f2c2070 6c617967 726f756e 64>

if let base64Encoded = utf8str?.base64EncodedStringWithOptions(NSDataBase64EncodingOptions(rawValue: 0))
{
    
    "Encoded:  \(base64Encoded)"//"Encoded:  SGVsbG8sIHBsYXlncm91bmQ="
    
    if let base64Decoded = NSData(base64EncodedString: base64Encoded, options:   NSDataBase64DecodingOptions(rawValue: 0))
        .map({ NSString(data: $0, encoding: NSUTF8StringEncoding) })
    {
        // Convert back to a string
        "Decoded:  \(base64Decoded)"//"Decoded:  Optional(Hello, playground)"
    }
}
</code>