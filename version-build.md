# version build

_Status: Published_
_Created: 2018-02-21 02:23:16_
_Tags: iOS swift_

<code>
if let version = Bundle.main.object(forInfoDictionaryKey: "CFBundleShortVersionString"),
            let build = Bundle.main.object(forInfoDictionaryKey: kCFBundleVersionKey as String)
 {
     versionLabel.text = "v\(version).\(build)"
}
</code>