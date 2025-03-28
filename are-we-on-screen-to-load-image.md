# Are we on screen to load image?

_Status: Published_
_Created: 2015-02-19 12:56:10_
_Tags: swift_

<code>
var imageURL: NSURL? {
    didSet{
      image = nil
      if view.window != nil { //Are we on screen?
          fetchImage()
      }
      
    }
  }
</code>