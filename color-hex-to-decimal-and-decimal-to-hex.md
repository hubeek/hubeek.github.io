# Color Hex to Decimal and Decimal to Hex

_Status: Published_
_Created: 2015-07-29 05:56:25_
_Tags: swift_

<code>

func colorCodeDecimalToHex(red:Int, green: Int, blue: Int) ->String
{
  var result = ""
  
  if red >= 0 && green >= 0 && blue >= 0 &&
  red <= 255 && green <= 255 && blue <= 255
  {
    result = "0x"
    result += NSString(format:"%2X", red) as String
    result += NSString(format:"%2X", green) as String
    result += NSString(format:"%2X", blue) as String
    return result.stringByReplacingOccurrencesOfString(" ", withString: "0")
    
  }
  
  return result
}

func colorCodeHexToRGB(hexString: String)-> String
{
  var result = ""
  var input = hexString.stringByReplacingOccurrencesOfString("0x", withString: "") as NSString
  
  var red = UInt8(strtoul(input.substringWithRange(NSRange(location: 0, length: 2)), nil, 16))
  var green = UInt8(strtoul(input.substringWithRange(NSRange(location: 2, length: 2)), nil, 16))
    var blue = UInt8(strtoul(input.substringWithRange(NSRange(location: 4, length: 2)), nil, 16))
  
  result = "\(red) \(green) \(blue)"
  return result
}

var a = colorCodeDecimalToHex(117, 186, 40) //"0x75BA28"
var b = colorCodeHexToRGB("0x75BA28")//"117 186 40"


</code>