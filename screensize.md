# ScreenSize

_Status: Published_
_Created: 2015-02-25 08:00:13_
_Tags: swift_

<code>
let screenSize: CGRect = UIScreen.mainScreen().bounds
let screenWidth = screenSize.width
let screenHeight = screenSize.height
</code>

general func:
<code>
func getScreenSize() ->CGRect {
    
    return UIScreen.mainScreen().bounds
    
}

func getScreenWidth() ->CGFloat {
    let screenSize: CGRect = UIScreen.mainScreen().bounds
    return screenSize.width
    
}

func getScreenHeight() ->CGFloat {
    let screenSize: CGRect = UIScreen.mainScreen().bounds
    return screenSize.height
}
</code>