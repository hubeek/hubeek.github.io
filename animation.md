# Animation

_Status: Published_
_Created: 2015-01-10 09:00:45_
_Tags: swift_

<code>override func viewDidAppear(animated: Bool) {
        
        UIView.animateWithDuration(1.0, animations: { () -> Void in
            
            self.image.center = CGPointMake(self.image.center.x + 400, self.image.center.y)
            self.image.alpha = 1.0
            self.image.frame = CGRectMake(0 , 0, 320, 320)
        })
    }
</code>