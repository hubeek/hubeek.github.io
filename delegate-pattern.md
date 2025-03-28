# Delegate pattern

_Status: Published_
_Created: 2015-08-13 03:13:40_
_Tags: swift_

delegation pattern
<code>
protocol ClassDelegate: class{
  func b1Pressed()
  
}
</code>
<br />
<code>
class Class: UIView
{

  weak var delegate: ClassDelegate?
...
func b1action(sender:UIButton)
  {
    self.delegate?. b1Pressed()
  }
</code>
<br />
<code>
class ViewController: UIViewController, ClassDelegate {

  override func viewDidLoad() {
    super.viewDidLoad()
    let class = Class(frame: CGRectMake(0, 0, 234, 234))
    menu.delegate = self
...

  }

...
  func b1Pressed() {
    println("clc")
  }
...
</code>

