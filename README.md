# Hack-Xcode

## Useful Features iOS Developers Should Know

### Customizing UINavigation & Status Bar
Put these lines of code to AppDeledate.swift under func didFinishLaunchingWithOptions 
```Swift
        UINavigationBar.appearance().barTintColor = UIColor(red: 42/255.0, green: 140/255.0, blue: 166/255.0, alpha: 0.5)
    
        UINavigationBar.appearance().barStyle = UIBarStyle.Default
    
        UINavigationBar.appearance().tintColor =  UIColor(red: 204/255.0, green: 255/255.0, blue: 204/255.0, alpha: 1)
    
        UINavigationBar.appearance().titleTextAttributes = [NSForegroundColorAttributeName: UIColor(red: 204/255.0, green: 255/255.0, blue: 204/255.0, alpha: 1), NSFontAttributeName: UIFont(name: "OpenSans-Bold", size: 25)!]
    
        UIApplication.sharedApplication().statusBarStyle = UIStatusBarStyle.LightContent
        return true
```
### Making a segue by pressing a button 
```Swift
        @IBAction func buttonPressed(sender: AnyObject) {
        performSegueWithIdentifier("goToSecond", sender: self)
        }
        //You must drag the button to another view controller and name the segue as "goToSecond" on the storyboard
```

### Passing Data to another viewController 
In the secondViewController, create a string variable called, "receviedString"
In the firstViewController, create a textfield and button that leads to the secondViewController

```Swift
        override func prepareForSegue(segue: UIStoryboardSegue, sender: AnyObject?) {
                var secondVC: secondViewController = segue.destinationViewController as! secondViewController 
                secondVC.receivedString = self.textField.text!
                }
        }
```
### Location Manager, MapKit, Annotation 
Getting the location of TajMahal. You need to import MapKit 

```Swift
    func getMapTajMahal() {
        //Coordinates
        let tajLat: CLLocationDegrees = 27.175015
        let tajLong: CLLocationDegrees = 78.042139
        let tajCoordinate = CLLocationCoordinate2D(latitude: tajLat, longitude: tajLat)
        
        //Span
        let latDelta: CLLocationDegrees = 0.01
        let longDelta: CLLocationDegrees = 0.01
        let tajSpan = MKCoordinateSpan(latitudeDelta: latDelta, longitudeDelta: longDelta)
        let tajRegion = MKCoordinateRegion(center: tajCoordinate, span: tajSpan)
        
        mapKitView.setRegion(tajRegion, animated: true)
        
        let tajAnnotation = MKPointAnnotation()
        tajAnnotation.title = "Hahah"
        tajAnnotation.subtitle = "Good"
        tajAnnotation.coordinate = tajCoordinate
        
        mapKitView.addAnnotation(tajAnnotation)
    }
```

### Location, Getting User's Current Location

```Swift 
import UIKit
import CoreLocation
import MapKit

class ViewController: UIViewController, MKMapViewDelegate, CLLocationManagerDelegate{

    var locationManager: CLLocationManager = CLLocationManager()
    
    
    @IBOutlet weak var mapKietView: MKMapView!
    override func viewDidLoad() {
        super.viewDidLoad()
        self.locationManager.delegate = self
        self.locationManager.desiredAccuracy = kCLLocationAccuracyBest
        self.mapKietView.showsUserLocation = true
        self.locationManager.requestAlwaysAuthorization()
        self.locationManager.startUpdatingLocation()
        mapKietView.showsUserLocation = true
        mapKietView.userTrackingMode = MKUserTrackingMode.Follow
        
        
    }

   //Location Delegate Methods 
    
    func locationManager(manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        let location = locations.last
        let center = CLLocationCoordinate2D(latitude: (location?.coordinate.latitude)!, longitude: (location?.coordinate.longitude)!)
        let region = MKCoordinateRegion(center: center, span: MKCoordinateSpan(latitudeDelta: 0.01, longitudeDelta: 0.01))
        self.mapKietView.setRegion(region, animated: true)
        self.locationManager.stopUpdatingLocation()
    }
    
    func locationManager(manager: CLLocationManager, didFailWithError error: NSError) {
        print("Error" + error.localizedDescription)
    }
    

}
```

