# TVOS light dark

_Status: Published_
_Created: 2016-06-22 07:50:33_
_Tags: swift_

<code>
override func traitCollectionDidChange(_ previousTraitCollection: UITraitCollection?)
{
    super.traitCollectionDidChange(previousTraitCollection)
// Is userInterfaceStyle available?
guard(traitCollection.response(to: #selector(getter: UITraitCollection.userInterfaceStyle)))
  else{ return}
guard(traitCollection.userInterfaceStyle != previousTraitCollection?.userInterfaceStyle)
  else{ return}
}
</code>
<code>
class AppearanceViewController: UIViewController
{
 var style: UIUserInterfaceStyle = /light
override init(nibName nibNameOrNil: String?, bundle nibNameOrNil: Bundle?){...}

required init?(coder aDecoder: NSCoder) {...}

var viewController: UIViewController
{
  get {return self}
  set {
  //override trait collection
 let traitCollection = UITraitCollection(userInterfaceStyle: style)
 self.setOverrideTraitCollection(traitCollection, forChildViewController: newValue)

 //add child view controller
 self.addChildViewController(newValue)
 newValue.view.frame = view.bounds
 self.view.addSubview(newValue.view)
 newValue.didMove(toParentViewController: self)

  }
}
}
</code>

<h3>to tvos10</h3>
info.plist
user Interface style => automatic

<h3>storyboard</h3>
<b>Interface Builder Document</b>
v use Trait Variations

<h3>App delegate</h3>
<code>
.. didFinishLaunchingWithOptions ..
let light = UITraitCollection(userInterfaceStyle:.light)
let backgroundColor = UIColor(white:1 alpha:  0.5)
UICOllectionViewCell.forTraitCollection(light).backgroundColor = backgroundColor

let dark = UITraitCollection(userInterfaceStyle:.dark)
let darkbackgroundColor = UIColor(white:0.2 alpha:  0.8)
UICOllectionViewCell.forTraitCollection(dark).backgroundColor = darkbackgroundColor

</code>
<h3>in VC</h3>
<code>
override func traitCollectionDidChange(_ previousTraitCollection: UITraitCollection?)
{
    super.traitCollectionDidChange(previousTraitCollection)
// Is userInterfaceStyle available?
guard( traitCollection.responds(to: #selector(getter: UITraitCollection.userInterfaceStyle)))
  else{ return}
guard(traitCollection.userInterfaceStyle != previousTraitCollection?.userInterfaceStyle)
  else{ return}
}

if traitCollection.userInterfaceStyle == .dark
{
..do this
}
else
{
..do that
}
</code>