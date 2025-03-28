# uialert

_Status: Published_
_Created: 2015-01-28 16:44:26_
_Tags: swift_

<code>
var alert = UIAlertController(title: "No Internetconnection", message: "U heeft een internet connctie nodig om aankopen te kunnen doen", preferredStyle: UIAlertControllerStyle.Alert)
    alert.addAction(UIAlertAction(title: "Opnieuw", style: UIAlertActionStyle.Default, handler: { (paramAction:UIAlertAction!) in
      
      self.fetchCreditStoreItems()
    }))
    alert.addAction(UIAlertAction(title: "Cancel", style: UIAlertActionStyle.Default, handler: { (paramAction:UIAlertAction!) in
      
      self.performSegueWithIdentifier("buyCreditsToHomeVC", sender: self)
    }))
    self.presentViewController(alert, animated: true, completion: nil)
</code>
met invullen
<code>
var controller:UIAlertController?
  
  override func viewDidLoad() {
    super.viewDidLoad()
    
    controller = UIAlertController(title: "Please enter your username",
      message: "This is usually 10 characters long",
      preferredStyle: .Alert)
    
    let action = UIAlertAction(title: "Next",
      style: UIAlertActionStyle.Default,
      handler: {[weak self] (paramAction:UIAlertAction!) in
        
        if let textFields = self!.controller?.textFields{
          let theTextFields = textFields as [UITextField]
          let userName = theTextFields[0].text
          println("Your username is \(userName)")
        }
        
      })
    
    controller!.addAction(action)
    
    controller!.addTextFieldWithConfigurationHandler(
      {(textField: UITextField!) in
        textField.placeholder = "XXXXXXXXXX"
      })
    
  }
  
  override func viewDidAppear(animated: Bool) {
    super.viewDidAppear(animated)
    self.presentViewController(controller!, animated: true, completion: nil)
  }
  

</code>

simpel
<code>

  var controller:UIAlertController?
  
  override func viewDidLoad() {
    super.viewDidLoad()
    
    controller = UIAlertController(title: "Title",
      message: "Message",
      preferredStyle: .Alert)
    
    let action = UIAlertAction(title: "Done",
      style: UIAlertActionStyle.Default,
      handler: {(paramAction:UIAlertAction!) in
      println("The Done button was tapped")
      })
    
    controller!.addAction(action)
    
  }
  
  override func viewDidAppear(animated: Bool) {
    super.viewDidAppear(animated)
    self.presentViewController(controller!, animated: true, completion: nil)
  }
</code>

met action
<code>
controller = UIAlertController(
      title: "Choose how you would like to share this photo",
      message: "You cannot bring back a deleted photo",
      preferredStyle: .ActionSheet)
    
    let actionEmail = UIAlertAction(title: "Via email",
      style: UIAlertActionStyle.Default,
      handler: {(paramAction:UIAlertAction!) in
        /* Send the photo via email */
      })
    
    let actionImessage = UIAlertAction(title: "Via iMessage",
      style: UIAlertActionStyle.Default,
      handler: {(paramAction:UIAlertAction!) in
        /* Send the photo via iMessage */
      })
    
    let actionDelete = UIAlertAction(title: "Delete photo",
      style: UIAlertActionStyle.Destructive,
      handler: {(paramAction:UIAlertAction!) in
        /* Delete the photo here */
      })
    
    controller!.addAction(actionEmail)
    controller!.addAction(actionImessage)
    controller!.addAction(actionDelete)
</code>

of...
<code>
var alert = UIAlertController(title: "Alert", message: "Message", preferredStyle: UIAlertControllerStyle.Alert)
alert.addAction(UIAlertAction(title: "Click", style: UIAlertActionStyle.Default, handler: nil))
self.presentViewController(alert, animated: true, completion: nil)
</code>
handle actions
<code>
alert.addAction(UIAlertAction(title: "Ok", style: .Default, handler: { action in
    switch action.style{
    case .Default:
        println("default")

    case .Cancel:
        println("cancel")

    case .Destructive:
        println("destructive")
    }
}))
</code>