# Remove Keyboard from view after typing txtField

_Status: Published_
_Created: 2015-01-10 09:56:45_
_Tags: swift_

<code>
 // MARK: delegtes
    
    func textFieldShouldReturn(textField: UITextField) -> Bool {
        textField.resignFirstResponder()
        return true
    }
    
    
    override func touchesBegan(touches: NSSet, withEvent event: UIEvent) {
        
        self.view.endEditing(true)
    }
    
</code>