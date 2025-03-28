# Link write review in app store

_Status: Published_
_Created: 2018-01-12 08:19:06_
_Tags: iOS swift_

<b>#available(iOS 10, *)!!!</b>
<code>
let appID = "959379869"

if let checkURL = URL(string: "http://itunes.apple.com/WebObjects/MZStore.woa/wa/viewContentsUserReviews?id=\(appID)&pageNumber=0&sortOrdering=2&type=Purple+Software&mt=8") {
    open(url: checkURL)
} else {
    print("invalid url")
}

...

func open(url: URL) {
    if #available(iOS 10, *) {
        UIApplication.shared.open(url, options: [:], completionHandler: { (success) in
            print("Open \(url): \(success)")
        })
    } else if UIApplication.shared.openURL(url) {
            print("Open \(url)")
    }
}
</code>