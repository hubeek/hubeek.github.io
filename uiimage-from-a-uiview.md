# UIImage from a UIView

_Status: Published_
_Created: 2018-06-09 01:41:31_
_Tags: swift iOS_

<code>
extension UIImage {
    // UIImage extension that creates a UIImage from a UIView
    convenience init (view:UIView) {
        UIGraphicsBeginImageContext(view.frame.size)
        view.layer.render(in: UIGraphicsGetCurrentContext()!)
        let image = UIGraphicsGetImageFromCurrentImageContext()
        UIGraphicsEndImageContext()
        self.init(cgImage: image!.cgImage!)
    }

}
</code>