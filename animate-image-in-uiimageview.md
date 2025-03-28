# Animate Image in UIImageView

_Status: Published_
_Created: 2015-02-26 06:37:36_
_Tags: swift_

<code>
for countValue in 1...20
    {
      
      var strImageName : String = countValue < 10 ?  "anim_jap000\(countValue).png" : "anim_jap00\(countValue).png"
      
      var image  = UIImage(named:strImageName)
      if image != nil{
        
        imgListArray.append(image!)
      }

      let animationImages:[AnyObject] = imgListArray
      imgView.animationImages = animationImages
      imgView.animationDuration = 1.5
      imgView.animationRepeatCount = 0
      imgView.startAnimating()
      //self.addSubview(loadingImageView)
</code>