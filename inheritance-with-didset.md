# Inheritance with didSet

_Status: Published_
_Created: 2015-11-15 06:54:53_
_Tags: swift_

<code>

class A:UIView
{
  var b:Int
  
  override init(frame: CGRect) {
    b = 1
    super.init(frame: frame)
  }

  required init?(coder aDecoder: NSCoder) {
      fatalError("init(coder:) has not been implemented")
  }
  
  func bla()
  {
    
  }

}

class B:A  {

  override var b:Int
  {
    didSet
    {
      print("b \(b)")
    }
  }

  func bcd()
  {
    
  }
  
  override func bla()
  {
    
  }

}
</code>