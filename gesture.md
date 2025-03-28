# Gesture

_Status: Published_
_Created: 2015-01-10 09:05:18_
_Tags: swift_

<code>var uilongPRec = UILongPressGestureRecognizer(target: self, action: "lpAction:")//funcName: : for adding var to fund!
        uilongPRec.minimumPressDuration = 1.5 //time for long press
        mapView.addGestureRecognizer(uilongPRec) // add long press to mapview

 func lpAction(gestureRecognizer: UIGestureRecognizer){
        
        var touchPoint = gestureRecognizer.locationInView(self.mapView)

        var newCoord:CLLocationCoordinate2D = self.mapView.convertPoint(touchPoint, toCoordinateFromView: self.mapView)
        
        var annotation:MKPointAnnotation = MKPointAnnotation()
        annotation.coordinate = newCoord
        annotation.title = "New Ann"
        annotation.subtitle = "One day I will come by"
        
        mapView.addAnnotation(annotation)
        
        
        
    }
</code>