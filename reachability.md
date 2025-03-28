# Reachability

_Status: Published_
_Created: 2015-10-06 08:26:40_
_Tags: swift_

<h5>swift 2.0</h5>
<code>
  
public class ReachabilityToConnection {
    class func isConnectedToNetwork() -> Bool {
      var zeroAddress = sockaddr_in()
      zeroAddress.sin_len = UInt8(sizeofValue(zeroAddress))
      zeroAddress.sin_family = sa_family_t(AF_INET)
      let defaultRouteReachability = withUnsafePointer(&zeroAddress) {
        SCNetworkReachabilityCreateWithAddress(nil, UnsafePointer($0))
      }
      var flags = SCNetworkReachabilityFlags()
      if !SCNetworkReachabilityGetFlags(defaultRouteReachability!, &flags) {
        return false
      }
      let isReachable = (flags.rawValue & UInt32(kSCNetworkFlagsReachable)) != 0
      let needsConnection = (flags.rawValue & UInt32(kSCNetworkFlagsConnectionRequired)) != 0
      return (isReachable && !needsConnection)
    }
}
</code>