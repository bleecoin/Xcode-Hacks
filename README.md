# Hack-Xcode

## Useful Features iOS Developers Should Know

### Customizing UINavigation & Status Bar
Put these lines of code to AppDeledate.swift under func didFinishLaunchingWithOptions 
```Swift
        UINavigationBar.appearance().barTintColor = UIColor.redColor
        UINavigationBar.appearance().barStyle = UIBarStyle.Default
        UINavigationBar.appearance().tintColor =  UIColor.redColor
        UINavigationBar.appearance().titleTextAttributes = [NSForegroundColorAttributeName: UIColor.redColor, NSFontAttributeName: UIFont(name: "OpenSans-Bold", size: 25)!]
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
### Adding a pop-over to a view controller
This is useful if you want to add and an invite feature or to indicate a level up. 
1. Make two UIViewControllers. The first controller has a button that will cause the second view to pop up. 
2. On the mainstoryboard, let the secondViewControllerID as "sbPopUpID" (any name you want) 

firstViewController (name: ViewController) 
```Swift 
        import UIKit
        class ViewController: UIViewController {
                @IBAction func showPopUp(sender: AnyObject) {
                        let popOverVC = UIStoryboard(name: "Main", bundle: nil).instantiateViewControllerWithIdentifier("sbPopUpID")
                        as! PopUpViewController
                
                //Adding secondView to the current view 
                self.addChildViewController(popOverVC)
                // Make the secondView's location and coordinate system relative to the firstView
                popOverVC.view.frame = self.view.frame
                self.view.addSubview(popOverVC.view)
                popOverVC.didMoveToParentViewController(self)
                }
        override func viewDidLoad() {
                super.viewDidLoad() 
        }
}
```
secondViewController (name: PopUpViewController) 
```Swift
        import Foundation
        import UIKit
        
        class PopUpViewController: UIViewController {
        override func viewDidLoad() {
                super.viewDidLoad() 
                self.view.backgroundColor = UIColor.blackColor().colorWithAlphaComponent(0.8)
                self.showAnimate()
                }
        @IBAction func closePopUp(sender: AnyObject) {
                self.removeAnimate() 
                }
        
        // Animation of the pop up
        func show Animate() {
                self.view.transform = CGAffineTransformMakeScale(1.2, 1.2)
                self.view.transform = CGAffineTransformMakeRotation(0.23)
                self.view.alpha = 0.0
                UIView.animateWithDuration(0.25, animations: {
                        self.view.alpha = 1.0
                        self.view.transform = CGAffineTransformMakeScale(1.0, 1.0)
                        })
        func removeAnimate() {
                UIView.animateWithDuration(0.25, animations: {
                        self.view.transform = CGAffineTransformMakeScale(1.3, 1.3)
                        self.view.alpha = 0.0 }, completion: {(finished: Bool) in 
                                if (finished) {
                                self.view.removeFromSuperView()
                                }
                        })
                }
        }
```
### Generation Random Number
```Swift 
        func randomInt(min: Int, max: Int) -> {
                return min + Int(arc4random_uniform(UInt32(max-min +1)
```
### Converting NSDate <-> Date(String)
```Swift 
        // NSDate to String 
        let date = NSDate() // Aug 10, 2016, 10:31PM
        let dateformatter = NSDateFormatter()
        dateFormatter.dateFormat = "dd-MM-yyyy"
        let todayDate: String = dateFormatter.stringFromDate(date)
        print(todayDate) // 10-08-2016
        
        // String to NSDate
        let todayDate = "10-08-2016"
        let newDateFormatter = NSDateFormatter()
        var dateFromString = dateFormatter.dateFromString(todayDate)
        print(dateFromString)
```

###Alert Controller 
```Swift
        LogOutAlert = UIAlertController(title: "Want to log out", message" "You sure?", preferredStyle: .Alert)
        // Creating LogOut Button
        let logOutAlertAction = UIAlertAction(title: "Log Out", style. Default, handler: { action in 
                let loginVieController: UIViewController = self.storyboard!.instantiateViewControllerWithIdentifir("login")
                self.presentViewController(loginViewController, animated: false, completion: nil) })
        
        // Create Cancel Button 
        let cancelAction = UIAlertAction(title: "Cancel", style .Cancel, handler: { action in 
                print("Cancel")
                self.navigationController?.popViewControllerAnimated(true) })
        
        logOUtAlert?.addAction(logOutAlertAction)
        logOUtAlert?.addAction(cancelAction)
        
        override func viewDidAppear(animated: Bool) {
                super.viewDidAppear(true)
                self.presentViewController(LogOUtAlert!, animated: true, completion: nil) 
                }
```
