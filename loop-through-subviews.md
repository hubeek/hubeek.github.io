# Loop through subviews

_Status: Published_
_Created: 2015-01-27 06:56:37_
_Tags: swift_

<code>
for view in self.view.subviews as [UIView] {
    if let textField = view as? UITextField {
        if textField.text == "" {
            // show error
            return
        }
    }
}
</code>