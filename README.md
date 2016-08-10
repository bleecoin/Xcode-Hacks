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
### Location Manager, MapKit
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

