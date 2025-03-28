# Text Spacing

_Status: Published_
_Created: 2016-10-07 02:33:49_
_Tags: swift_

<code>

extension UILabel{
    func addTextSpacing(spacing: CGFloat){
        let attributedString = NSMutableAttributedString(string: self.text!)
        attributedString.addAttribute(NSKernAttributeName, value: spacing, range: NSRange(location: 0, length: self.text!.characters.count))
        self.attributedText = attributedString
    }
}
</code>
cell.titleLabel.addTextSpacing(1.4)