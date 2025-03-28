# Data Compression

_Status: Published_
_Created: 2019-06-07 02:34:44_
_Tags: iOS swift_

<code>
let compressed = try data.compressed(using: .zlib)
public enum CompressionAlgorithm: Int {
  case lzfse
  case lz4
  case lama
  case zlib
}
</code>