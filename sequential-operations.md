# Sequential Operations

_Status: Published_
_Created: 2019-05-19 14:27:17_
_Tags: iOS_

<code>
class DownloadOperation : Operation {
    
    private var task : URLSessionDownloadTask!
    
    enum OperationState : Int {
        case ready
        case executing
        case finished
    }
    
    // default state is ready (when the operation is created)
    private var state : OperationState = .ready {
        willSet {
            self.willChangeValue(forKey: "isExecuting")
            self.willChangeValue(forKey: "isFinished")
        }
        
        didSet {
            self.didChangeValue(forKey: "isExecuting")
            self.didChangeValue(forKey: "isFinished")
        }
    }
    
    override var isReady: Bool { return state == .ready }
    override var isExecuting: Bool { return state == .executing }
    override var isFinished: Bool { return state == .finished }
    
    init(session: URLSession, downloadTaskURL: URL, completionHandler: ((URL?, URLResponse?, Error?) -> Void)?) {
        super.init()
        
        task = session.downloadTask(with: downloadTaskURL, completionHandler: { [weak self] (localURL, response, error) in
            
            /*
             if there is a custom completionHandler defined,
             pass the result gotten in downloadTask's completionHandler to the
             custom completionHandler
             */
            if let completionHandler = completionHandler {
                // localURL is the temporary URL the downloaded file is located
                completionHandler(localURL, response, error)
            }
            
            /*
             set the operation state to finished once
             the download task is completed or have error
             */
            self?.state = .finished
        })
    }
    
    override func start() {
        /*
         if the operation or queue got cancelled even
         before the operation has started, set the
         operation state to finished and return
         */
        if(self.isCancelled) {
            state = .finished
            return
        }
        
        // set the state to executing
        state = .executing
        
        print("downloading \(self.task.originalRequest?.url?.absoluteString ?? "")")
            
            // start the downloading
            self.task.resume()
    }
    
    override func cancel() {
        super.cancel()
        
        // cancel the downloading
        self.task.cancel()
    }
}
</code>
use it in vc:
<code>class ViewController: UIViewController {

    @IBOutlet weak var downloadButton: UIButton!
    
    @IBOutlet weak var progressLabel: UILabel!
    
    @IBOutlet weak var cancelButton: UIButton!
    
    var session : URLSession!
    var queue : OperationQueue!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view, typically from a nib.
        
        session = URLSession(configuration: URLSessionConfiguration.default, delegate: nil, delegateQueue: nil)
        queue = OperationQueue()
        queue.maxConcurrentOperationCount = 1
        
        self.cancelButton.isEnabled = false
    }

    @IBAction func downloadTapped(_ sender: UIButton) {
        let completionOperation = BlockOperation {
            print("finished download all")
            DispatchQueue.main.async {
                self.cancelButton.isEnabled = false
            }
        }
        
        let urls = [
            URL(string: "https:/...zip")!,
            URL(string: "https:/...zip")!,
            URL(string: "https:/...zip")!,
            URL(string: "https:/...zip")!,
            URL(string: "https:/...zip")!,
        ]
        
        for (index, url) in urls.enumerated() {
            let operation = DownloadOperation(session: self.session, downloadTaskURL: url, completionHandler: { (localURL, urlResponse, error) in
                
                if error == nil {
                    DispatchQueue.main.async {
                        self.progressLabel.text = "\(index + 1) / \(urls.count) files downloaded"
                    }
                }
            })
            
            completionOperation.addDependency(operation)
            self.queue.addOperation(operation)
        }
        
        self.queue.addOperation(completionOperation)
        self.cancelButton.isEnabled = true
    }
    
    @IBAction func cancelTapped(_ sender: UIButton) {
        queue.cancelAllOperations()
        
        self.progressLabel.text = "Download cancelled"
        
        self.cancelButton.isEnabled = false
    }
    
}</code>