# uimaps location and annotation

_Status: Published_
_Created: 2015-01-10 09:12:18_
_Tags: swift_

<code>class ViewController: UIViewController, MKMapViewDelegate, CLLocationManagerDelegate {

    @IBOutlet var mapView: MKMapView!
    
    var manager:CLLocationManager
    
    
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view, typically from a nib.
        
        //core location
        manager.delegate = self
        manager.desiredAccuracy = kCLLocationAccuracyBest
        manager.requestWhenInUseAuthorization()
        manager.startUpdatingLocation()
        
        
        var lat:CLLocationDegrees = 40.748473
        var long:CLLocationDegrees = -73.985417
        
        var latDelta:CLLocationDegrees = 0.01
        var longDelta:CLLocationDegrees = 0.01
        
        var span:MKCoordinateSpan = MKCoordinateSpanMake(latDelta, longDelta)
        var location:CLLocationCoordinate2D = CLLocationCoordinate2DMake(lat, long)
        
        var region:MKCoordinateRegion = MKCoordinateRegionMake(location, span)
        mapView.setRegion(region, animated: true)
        
        var annotation:MKPointAnnotation = MKPointAnnotation()
        annotation.coordinate = location
        annotation.title = "Statue of Liberty"
        annotation.subtitle = "One day I will come by"
        
        mapView.addAnnotation(annotation)
        
        
    }
</code>