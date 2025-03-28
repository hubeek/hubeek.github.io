# ZoomableGridVC

_Status: Published_
_Created: 2016-12-13 02:49:48_
_Tags: swift_

<code>
enum GridFillDirection
{
    case Horizontal, Vertical
}

class ZoomableGridViewController: UIViewController,UIScrollViewDelegate {
    
    //MARK: - Properties
    
    var scrollView: UIScrollView!
    var scrollIsZoomedIn = false
    var gridView: UIView!//Grid!//or image etc
    
    var puzzleDirection:GridFillDirection = .Horizontal
    
    var logText:UILabel!
    
    //MARK: - VC
    override func viewDidLoad() {
        super.viewDidLoad()
        
        gridView = UIImageView(image: UIImage(named: "nasa_big"))//UIView(frame: CGRectMake(0,0,view.bounds.width,view.bounds.width))//
        
        scrollView = UIScrollView(frame: CGRectMake(0,80,view.bounds.width,view.bounds.width))
        scrollView.backgroundColor = UIColor.blackColor()
        scrollView.contentSize = gridView.bounds.size
        scrollView.autoresizingMask = UIViewAutoresizing.FlexibleWidth
        scrollView.delegate = self
        scrollView.maximumZoomScale = 4.0
        setZoomScale()
        scrollView.contentOffset = CGPoint(x: 0, y: 0)
        scrollView.addSubview(gridView)
        view.addSubview(scrollView)
        
        setupGestureRecognizer()
        
        setupLogText()
    }
    
    //MARK: - Setup Layout
    func setupLogText()
    {
        let logtextHeight:CGFloat = 40
        logText = UILabel(frame: CGRectMake(0,view.bounds.height-logtextHeight,view.bounds.width,logtextHeight))
        logText.textAlignment = .Center
        view.addSubview(logText)
        createLogText()
    }
    
    func createLogText()
    {
        let text = (puzzleDirection == .Horizontal) ? "Hori" :  "Verti"
        logText.text = "\(text) zoom : \(scrollView.zoomScale) "
    }
    
    func setZoomScale() {
        
        let widthScale = scrollView.bounds.size.width / gridView.bounds.size.width
        let heightScale = scrollView.bounds.size.height / gridView.bounds.size.height
        
        scrollView.minimumZoomScale = min(widthScale, heightScale)
        scrollView.zoomScale = widthScale
    }
    
    //MARK: - ScrollView delegates
    func viewForZoomingInScrollView(scrollView: UIScrollView) -> UIView? {
        return gridView
    }
    
    func scrollViewDidZoom(scrollView: UIScrollView) {
        
        let verticalPadding = gridView.bounds.size.height < scrollView.bounds.size.height ? (scrollView.bounds.size.height - gridView.bounds.size.height) / 2 : 0
        let horizontalPadding = gridView.bounds.size.width < scrollView.bounds.size.width ? (scrollView.bounds.size.width - gridView.bounds.size.width) / 2 : 0
        
        scrollView.contentInset = UIEdgeInsets(top: verticalPadding, left: horizontalPadding, bottom: verticalPadding, right: horizontalPadding)
        
    }
    
    //MARK: - Gestures
    func setupGestureRecognizer() {
        let doubleTap = UITapGestureRecognizer(target: self, action: #selector(ZoomableGridViewController.handleDoubleTap(_:)))
        doubleTap.numberOfTapsRequired = 2
        scrollView.addGestureRecognizer(doubleTap)
        
        let singleTap = UITapGestureRecognizer(target: self, action: #selector(ZoomableGridViewController.handleSingleTap(_:)))
        singleTap.numberOfTapsRequired = 1
        scrollView.addGestureRecognizer(singleTap)
        
        let swipeRight = UISwipeGestureRecognizer(target: self, action: #selector(ZoomableGridViewController.handleSwipeGesture(_:)))
        swipeRight.direction = UISwipeGestureRecognizerDirection.Right
        self.view.addGestureRecognizer(swipeRight)
        
        let swipeDown = UISwipeGestureRecognizer(target: self, action: #selector(ZoomableGridViewController.handleSwipeGesture(_:)))
        swipeDown.direction = UISwipeGestureRecognizerDirection.Down
        self.view.addGestureRecognizer(swipeDown)
        
        let swipeLeft = UISwipeGestureRecognizer(target: self, action: #selector(ZoomableGridViewController.handleSwipeGesture(_:)))
        swipeLeft.direction = UISwipeGestureRecognizerDirection.Left
        self.view.addGestureRecognizer(swipeLeft)
        
        let swipeUp = UISwipeGestureRecognizer(target: self, action: #selector(ZoomableGridViewController.handleSwipeGesture(_:)))
        swipeUp.direction = UISwipeGestureRecognizerDirection.Up
        self.view.addGestureRecognizer(swipeUp)
        
    }
    
    func handleSwipeGesture(gesture: UIGestureRecognizer) {
        
        if let swipeGesture = gesture as? UISwipeGestureRecognizer {
            
            createLogText()
            switch swipeGesture.direction {
            case UISwipeGestureRecognizerDirection.Right:
                
                logText.text? += "Swiped right select next horizontal region"
                if swipeGesture.state == UIGestureRecognizerState.Began
                {
                    
                }
                
            case UISwipeGestureRecognizerDirection.Down:
                
                logText.text? += "Swiped down select next vertical region"
                
                
            case UISwipeGestureRecognizerDirection.Left:
                
                logText.text? += "Swiped left select previous horizontal region"
                
                
            case UISwipeGestureRecognizerDirection.Up:
                
                
                logText.text? += "Swiped up select previous vertical region"
                
                
            default:
                break
            }
        }
    }
    
    func checkZoomState()
    {
        let widthScale = scrollView.bounds.size.width / gridView.bounds.size.width
        if widthScale == scrollView.zoomScale
        {
            //print("zoom scale full")
            scrollIsZoomedIn = false
        }
        else
        {
            //print("zoom scale zoomed")
            scrollIsZoomedIn = true
        }
    }
    
    func handleSingleTap(recognizer: UITapGestureRecognizer)
    {
        checkZoomState()
        createLogText()
        if scrollIsZoomedIn
        {
            logText.text? += "singleTap - selected cell if selected change direction"
        }
        else
        {
            logText.text? += "singleTap - selected cell "
        }
    }
    
    func handleDoubleTap(recognizer: UITapGestureRecognizer) {
        //print("double tap")
        checkZoomState()
        createLogText()
        if puzzleDirection == .Horizontal
        {
            puzzleDirection = .Vertical
        }
        else
        {
            puzzleDirection = .Horizontal
        }
     
    }
  
}
</code>