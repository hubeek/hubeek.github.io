# twitter tweet

_Status: Published_
_Created: 2015-05-19 05:55:24_
_Tags: swift_

<code>
if SLComposeViewController.isAvailableForServiceType(SLServiceTypeTwitter)
    {
      
      var controller = SLComposeViewController(forServiceType: SLServiceTypeTwitter)
      controller.setInitialText("Solved a Sudoku! ")
      controller.addImage(UIImage(named: "solvedImage"))
      controller.addURL(NSURL(string: "http://www.megastar-games.com"))
      controller.completionHandler = {
        (result:SLComposeViewControllerResult) in
       
        println("twit finished")
      }
      self.presentViewController(controller, animated: true, completion: nil)
    }
    else
    {
      println("twit not available")
    }
</code>