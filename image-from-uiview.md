# Image from UIView

_Status: Published_
_Created: 2018-02-16 10:01:40_
_Tags: iOS swift_

<code>
func imageWithView(inView: UIView) -> UIImage? {
    UIGraphicsBeginImageContextWithOptions(inView.bounds.size, inView.isOpaque, 0.0)
    defer { UIGraphicsEndImageContext() }
    if let context = UIGraphicsGetCurrentContext() {
        inView.layer.render(in: context)
        let image = UIGraphicsGetImageFromCurrentImageContext()
        return image
    }
    return nil
}
</code>