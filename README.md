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


