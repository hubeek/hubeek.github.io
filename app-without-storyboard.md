# App without Storyboard

_Status: Published_
_Created: 2016-03-24 06:53:20_
_Tags: swift_

<h2>iOS 14</h2>
<ul>
<li>remove main story board from files</li>
<li>from <app-name> => info remove 'main storyboard file base name'</li>
<li>then drill down in scene manifest to remove main item 0 main file name and remove</li>
</ul>
adjust code in sceneDelegate:
<code>
class SceneDelegate: UIResponder, UIWindowSceneDelegate {

    var window: UIWindow?


    func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
        guard let windowScene = (scene as? UIWindowScene) else { return }
        let window = UIWindow(windowScene: windowScene)
        window.rootViewController = ViewController()
        window.makeKeyAndVisible()
        self.window = window
    }
...
</code>
<h2>Project > Targets > Deployment Info</h2>
<p>empty "Main Interface"</p>
<h2>Remove Reference in Info.plist</h2>
<p>
Open your Info.plist
<li>
<ul>Click the arrow at the leftmost of Application Scene Manifest (UIApplicationSceneManifest) key to expand</ul>
<ul>Click the arrow at the leftmost of Scene Configuration (UISceneConfigurations) key to expand</ul>
<ul>Click the arrow at the leftmost of Application Session Role (UIWindowSceneSessionRoleApplication) key to expand</ul>
<ul>Click the arrow at the leftmost of First Item (Item 0) key to expand</ul>
<ul>Remove the key Storyboard Name (UISceneStoryboardFile)</ul>
</li>

<h2>From IOS 13</h2>
<p>
Not in appDelegate anymore...
in SceneDelegate:
<code>
func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
        // Use this method to optionally configure and attach the UIWindow `window` to the provided UIWindowScene `scene`.
        // If using a storyboard, the `window` property will automatically be initialized and attached to the scene.
        // This delegate does not imply the connecting scene or session are new (see `application:configurationForConnectingSceneSession` instead).
        guard let windowScene = (scene as? UIWindowScene) else { return }
        window = UIWindow(windowScene: windowScene)
        window?.rootViewController = MockupIntroVC()
        window?.backgroundColor = .systemBackground // optional
        window?.makeKeyAndVisible()
    }</code>
</p>
<h2>AppDelegate</h2>
<code>
var window: UIWindow?

  func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
    window = UIWindow(frame: UIScreen.mainScreen().bounds)
    if let window = window {
      window.backgroundColor = UIColor.whiteColor()
      window.rootViewController = ViewController()
      window.makeKeyAndVisible()
    }
    return true
  }

</code>
<h2>ViewController</h2>
<code>
class ViewController: UIViewController {

  var button :UIButton!
  

  override func viewDidLoad() {
    super.viewDidLoad()
    
    // Do any additional setup after loading the view, typically from a nib.
    view.backgroundColor = .redColor()
    setupLayout()
  }
  
 
  func setupLayout()
  {
    if button == nil
    {
      self.view.addSubview(createButton(self))
      }
  }

  func buttonPressed(sender:UIButton)
  {
    showNewViewController(SecondViewController())
  }
  override func didReceiveMemoryWarning() {
    super.didReceiveMemoryWarning()
    // Dispose of any resources that can be recreated.
    print("\(__FUNCTION__)")
  }

  deinit
  {
    print("\(__FUNCTION__) v1")
  }

}

// General funcs for demo purposes
func createButton(vc:UIViewController)->UIButton
{
  let button:UIButton
  button = UIButton(frame: CGRectMake(0,0,123,123))
  button.backgroundColor = .yellowColor()
  button.addTarget(vc, action: "buttonPressed:", forControlEvents: .TouchUpInside)
  button.setTitle("Button", forState: .Normal)
  return button
}

func showNewViewController(vc:UIViewController)
{
  UIApplication.sharedApplication().keyWindow!.rootViewController = vc.self
 
}
</code>
<h2> SecondViewController </h2>
<code>
class SecondViewController: UIViewController {

  var button :UIButton!
  override func viewDidLoad() {
    super.viewDidLoad()
    // Do any additional setup after loading the view, typically from a nib.
    view.backgroundColor = .blueColor()
    setupLayout()
      }

  override func didReceiveMemoryWarning() {
    super.didReceiveMemoryWarning()
    // Dispose of any resources that can be recreated.
  }


  func setupLayout()
  {
    if button == nil
    {
      self.view.addSubview(createButton(self))
    }
  }
  
  func buttonPressed(sender:UIButton)
  {
    showNewViewController(ViewController())
  }
  deinit
  {
    print("\(__FUNCTION__) v2")
  }
}

</code>