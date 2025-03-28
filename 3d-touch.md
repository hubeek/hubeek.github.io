# 3d touch

_Status: Published_
_Created: 2016-06-08 04:23:44_
_Tags: swift_

Voor icon on 'desktop'

In info.plist
add:
<code>
<key>UIApplicationShortcutItems</key>
	<array>
		<dict>
			<key>UIApplicationShortcutItemIconFile</key>
			<string>button_continue</string>
			<key>UIApplicationShortcutItemSubtitle</key>
			<string>Continue last puzzle</string>
			<key>UIApplicationShortcutItemTitle</key>
			<string>Continue</string>
			<key>UIApplicationShortcutItemType</key>
			<string>com.company.bla.bla</string>
		</dict>
		<dict>
			<key>UIApplicationShortcutItemIconFile</key>
			<string>button_puzzles</string>
			<key>UIApplicationShortcutItemSubtitle</key>
			<string>Choose new puzzle</string>
			<key>UIApplicationShortcutItemTitle</key>
			<string>New puzzle</string>
			<key>UIApplicationShortcutItemType</key>
			<string>com.company.bla.bla</string>
		</dict>
	</array>
</code>

<br />
<br />
<p>
<b>in UIView</b>
<code>
import UIKit
import AudioToolbox

protocol SelectLetterViewDelegate: class
{
    func foundChar(foundChar:String)
    func addChar(foundChar:String)
}

class SelectLetterView:UIView
{
    
    weak var delegate: SelectLetterViewDelegate?
    
    var charsToChoose =
        [">","A","B","C","D","E","F",
         "G","H","I","J","K","L",
         "M","N","O","P","Q","R",
         "S","T","U","V","W","X",
         "Y","Z","*"
    ]
    var lastChosenString = ""
    var charCollection: [UILabel] = []
 
    var clickon = false
    var useForceTouch = false
    
    //Mark: - Init / setup
    override init(frame: CGRect) {
        super.init(frame: frame)
        
        self.initialize()
    }
    
    convenience init() {
        self.init(frame: CGRectZero)
        
        self.initialize()
    }
    
    required init?(coder aDecoder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
    func initialize() {
        addCharsToView()
        print("traitCollection.forceTouchCapability \(traitCollection.forceTouchCapability)")
        if traitCollection.forceTouchCapability == UIForceTouchCapability.Available
        {
            print("we have forceTouchCapability")
            useForceTouch = true
        }
        else
        {
            print("we dont have forceTouchCapability...")
        }
    }
    
    //Mark: - Layout
    func addCharsToView()
    {
        if charsToChoose.count > 0
        {
            let dimensionHeight:CGFloat = self.frame.height / CGFloat(charsToChoose.count)
            for i in 0 ..< charsToChoose.count
            {
                let view = UILabel(frame: CGRectMake(0,CGFloat(i) * dimensionHeight,self.frame.width,dimensionHeight))
                if i%2==0
                {
                    view.backgroundColor = .darkGrayColor()
                }
                else
                {
                    view.backgroundColor = .clearColor()
                }
                view.text = "\(charsToChoose[i])"
                view.textColor = .whiteColor()
                view.textAlignment = .Center
                charCollection.append(view)
                self.addSubview(view)
            }
        }
    }
    
    
    //Mark: - Touches
    override func touchesBegan(touches: Set<UITouch>, withEvent event: UIEvent?) {
        reactToTouch(touches, withEvent: event)
    }
    
    override func touchesMoved(touches: Set<UITouch>, withEvent event: UIEvent?) {
        reactToTouch(touches, withEvent: event)
    }
    
    override func touchesEnded(touches: Set<UITouch>, withEvent event: UIEvent?) {
        reactToTouch(touches, withEvent: event)
    }
    var canAddChar                      = false
    var lastFractionPressure:CGFloat    = 0
    
    func reactToTouch(touches: Set<UITouch>, withEvent event: UIEvent?)
    {
        
        if let touch = touches.first
        {
            let fractionTouchPressure = touch.force/touch.maximumPossibleForce
            if fractionTouchPressure >= 1.0 && touch.force > 0 && touch.maximumPossibleForce > 0 && clickon == false && lastFractionPressure == 0
            {
                lastFractionPressure = fractionTouchPressure
                clickon = true
                canAddChar = true
                AudioServicesPlaySystemSound(kSystemSoundID_Vibrate)
                dispatch_after(200, dispatch_get_main_queue())
                {
                    AudioServicesDisposeSystemSoundID(kSystemSoundID_Vibrate)
                }
                print("click On \(touch.force/touch.maximumPossibleForce)")
                
            }
            if clickon == true && fractionTouchPressure <= 0.2
            {
                print("click off")
                clickon = false
                lastFractionPressure = 0
            }
            let position :CGPoint = touch.locationInView(self)
            if event != nil
            {
                foundCharOnTouch(position,event: event!, clickon: clickon)
            }
        }
    }
    
    func foundCharOnTouch(point:CGPoint,event:UIEvent,clickon:Bool)
    {
        for l in self.subviews
        {
            if l is UILabel
            {
                if let label = l as? UILabel
                {
                    
                    if label.pointInside(convertPoint(point, toView: label), withEvent: event)
                    {
                        lastChosenString = label.text!
                        if clickon == false
                        {
                            delegate?.foundChar(label.text!)
                        }
                        else
                        {
                            if lastFractionPressure != 0 && canAddChar
                            {
                                canAddChar = false
                                delegate?.addChar(label.text!)
                                
                            }
                        }
                    }
                }
            }
           
        }
    }
}
</code>
</p>

<b>AppDelegate</b>

<code>
import UIKit


enum DGShortcutItemType: String {
    case Continue
    case NewPuzzle
    
    init?(shortcutItem: UIApplicationShortcutItem) {
        guard let last = shortcutItem.type.componentsSeparatedByString(".").last else { return nil }
        self.init(rawValue: last)
    }
    
    var type: String {
        return NSBundle.mainBundle().bundleIdentifier! + ".\(self.rawValue)"
    }
}

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?


    func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
        if let shortcutItem = launchOptions?[UIApplicationLaunchOptionsShortcutItemKey] as? UIApplicationShortcutItem {
            handleShortcutItem(shortcutItem)
        }
        return true
    }


    func application(application: UIApplication, performActionForShortcutItem shortcutItem: UIApplicationShortcutItem, completionHandler: (Bool) -> Void) {
        handleShortcutItem(shortcutItem)
    }

    private func handleShortcutItem(shortcutItem: UIApplicationShortcutItem) {
        if let rootViewController = window?.rootViewController, let shortcutItemType = DGShortcutItemType(shortcutItem: shortcutItem) {
            rootViewController.dismissViewControllerAnimated(false, completion: nil)
            let alertController = UIAlertController(title: "", message: "", preferredStyle: .Alert)
            
            switch shortcutItemType {
            case .Continue:
                alertController.message = "Continue"
                break
            case .NewPuzzle:
                alertController.message = "New Puzzle"
                break
            }
            
            alertController.addAction(UIAlertAction(title: "OK", style: .Default, handler: nil))
            rootViewController.presentViewController(alertController, animated: true, completion: nil)
        }
    }
}
</code>