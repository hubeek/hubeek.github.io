# time for timer calc

_Status: Published_
_Created: 2015-04-05 13:46:37_
_Tags: swift_

<code>
    let minutes:Int = Int( Float(elapsedTime) / 60.0 )
    let hours:Int = Int( Float(elapsedTime) / 3600.0 )
    let sec:Int = Int( fmodf(Float(elapsedTime), 60.0))

    var minuteStr = "\(minutes)"
    if minutes < 10 {
      minuteStr = "0\(minutes)"
    }
    var hourStr = "\(hours)"
    if hours < 10 {
      hourStr = "0\(hours)"
    }
    var secStr = "\(sec)"
    if sec < 10 {
      secStr = "0\(sec)"
    }
    
    timeLabel.text = "\(hourStr):\(minuteStr):\(secStr)"

</code>