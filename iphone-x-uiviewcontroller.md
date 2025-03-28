# iPhone x uiviewcontroller

_Status: Published_
_Created: 2018-02-16 06:26:43_
_Tags: iOS swift_

<code>
class BaseVC: UIViewController
{
   var shouldHideHomeIndicator     = false
   public let stage                = UIView()

   override func viewDidLoad() {
       super.viewDidLoad()
       HLog.info(function:#function, message: "BaseVC")

       navigationController?.setToolbarHidden(true, animated: false)
       navigationController?.navigationBar.isHidden = true

       setupLayout()
   }


   override func viewDidAppear(_ animated: Bool) {
       super.viewDidAppear(animated)

       self.shouldHideHomeIndicator = true
       if #available(iOS 11.0, *) {
           self.setNeedsUpdateOfHomeIndicatorAutoHidden()
       } else {
           // Fallback on earlier versions
       }
   }

   override var prefersStatusBarHidden: Bool
   {
       return true
   }

   override func preferredScreenEdgesDeferringSystemGestures() ->
UIRectEdge {
       return .top
   }

   override func prefersHomeIndicatorAutoHidden() -> Bool
   {
       return shouldHideHomeIndicator
   }
   //MARK: - Layout
   func setupLayout()
   {
       createStage()
   }

   func createStage()
   {

       let ninesixteen = (sw/9.0*16.0).rounded()
       if ninesixteen <= sh
       {
           stage.frame = Frame(x: 0, y: 0, width: sw, height: ninesixteen)
       }
       else
       {
           stage.frame = Frame(x: 0, y: 0, width: sh/16.0*9.0, height: sh)
       }
       stage.backgroundColor = .clear
       stage.center = view.center
       view.addSubview(stage)
   }

   //MARK: - Helper
   func goto(vc:UIViewController)
   {
       AudioPlayerHelper.play(audioButtonClick)
       UIApplication.shared.keyWindow?.rootViewController = vc.self
   }
}
</code>