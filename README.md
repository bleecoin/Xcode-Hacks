# Hack-Xcode

## Useful Features iOS Developers Should Know

### Customizing UINavigation & Status Bar
Put these lines of code to AppDeledate.swift under func didFinishLaunchingWithOptions 

    UINavigationBar.appearance().barTintColor = UIColor(red: 42/255.0, green: 140/255.0, blue: 166/255.0, alpha: 0.5)

    UINavigationBar.appearance().barStyle = UIBarStyle.Default

    UINavigationBar.appearance().tintColor =  UIColor(red: 204/255.0, green: 255/255.0, blue: 204/255.0, alpha: 1)

    UINavigationBar.appearance().titleTextAttributes = [NSForegroundColorAttributeName: UIColor(red: 204/255.0, green: 255/255.0, blue: 204/255.0, alpha: 1), NSFontAttributeName: UIFont(name: "OpenSans-Bold", size: 25)!]//UIColor(red: 42/255.0, green: 140/255.0, blue: 166/255.0, alpha: 1.0)

    UIApplication.sharedApplication().statusBarStyle = UIStatusBarStyle.LightContent
    return true
    




