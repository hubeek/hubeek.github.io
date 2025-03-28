# UILabel outlined / stroked text

_Status: Published_
_Created: 2017-10-20 02:50:46_
_Tags: swift_

<code>
class StrokedLabel: UILabel {
    
    var strockedText: String = "" {
        willSet(newValue) {
            let strokeTextAttributes = [
                NSAttributedStringKey(rawValue: NSAttributedStringKey.strokeColor.rawValue) : UIColor.black,
                NSAttributedStringKey(rawValue: NSAttributedStringKey.foregroundColor.rawValue) : UIColor.white,
                NSAttributedStringKey(rawValue: NSAttributedStringKey.strokeWidth.rawValue) : -4.0,
                NSAttributedStringKey(rawValue: NSAttributedStringKey.font.rawValue) : UIFont.boldSystemFont(ofSize: 30)
                ] as [NSAttributedStringKey : Any]?
            
            let customizedText = NSAttributedString(string: newValue
                , attributes: strokeTextAttributes)
            
            
            
            attributedText = customizedText
        }
    }
}
</code>