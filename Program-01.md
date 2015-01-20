### Getting Started

1. Open Xcode IDE (Integrated Development Environment) 
2. Chose new Xcode project using the single-view application template, and make sure you opt for Swift as the language.
3. Find an `AppDelegate.swift` file in the project hierarchy. Inside of this file find the line that says:

```swift
“// Override point for customization after application launch.”
```

Replace this line with our amazing hello world code:
```swift
println("Hello World")
```

Now press run and you should see a blank app boot up, and the words “Hello World” print to the console. 

### Adding a Table View
In this section, we’re going to actually put some stuff on the screen, yay!

Open up your Main.storyboard file in Xcode and lets drag in a “Table View” object from the Object Library. Position this fullscreen in your app window and make sure it lines up with the edges. If you run the app at this point, you should see an empty table view in the simulator.

Now we need to set up a delegate and data source for the table view. This is easy to do in interface builder. Just hold control, and then click and drag from the tableview to the “View Controller” object in your storyboard’s hierarchy, and select ‘data source’. Repeat with the ‘delegate’ options.

Okay, now let’s dig in to the protocol methods for Table Views. Because we’re using the UITableViewDataSource and UITableViewDelegate in our view controller, we need to modify the class definition to say as much.

So open ViewController.swift and modify this line:

```swift
class ViewController: UIViewController {
```

to this:


```
class ViewController: UIViewController, UITableViewDataSource, UITableViewDelegate {
```

Command+clicking on either of these protocols will show the required functions at the very top. In the case of a tableview, we need at least these two:


```
func tableView(tableView: UITableView!, numberOfRowsInSection section: Int) -> Int
func tableView(tableView: UITableView!, cellForRowAtIndexPath indexPath: NSIndexPath!) -> UITableViewCell!
```

So let’s modify our View Controller class by adding these two functions


```swift
func tableView(tableView: UITableView!, numberOfRowsInSection section:    Int) -> Int {
return 10
}


func tableView(tableView: UITableView!, cellForRowAtIndexPath indexPath: NSIndexPath!) -> UITableViewCell! {
let cell: UITableViewCell = UITableViewCell(style: UITableViewCellStyle.Subtitle, reuseIdentifier: "MyTestCell")

cell.text = “Row #\(indexPath.row)”
cell.detailTextLabel.text = “Subtitle #\(indexPath.row)”

return cell
}
```

The first method is asking for the number of rows in our section, in this simple iOS 8 Hello World tutorial we just hard-code 10, but normally it would be the length of an array controller. This example is intentionally simple.

The second method is where the magic happens. Here we create a new instance of a UITableViewCell called cell, using the Subtitle cell style.

Then, we assign the text value of this cell to the string “Row #\(indexPath.row)”

In iOS8 Swift, this is how variables are embedded within a string. What we’re doing is retrieving the value of indexPath.row by inserting \(indexPath.row) in to our string, and dynamically replacing it with the row number of the cell. This allows results such as “Row #1″, “Row #2″, etc.

The detail text label is only available in the Subtitle cell class, which we are using here. We set it similarly to “Subtitle #1″, “Subtitle #2″, and so on.

Go ahead and run your iOS8 Hello World app and you’ll now see an amazing list of cells with titles and subtitles indicating their row numbers. This is one of the most common ways to display data in iOS, and will be sure to serve you well. For the full code to my View Controller file, take a look here:


```swift
import UIKit
 
class ViewController: UIViewController, UITableViewDataSource, UITableViewDelegate {
                            
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view, typically from a nib.
    }
 
    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
    
    func tableView(tableView: UITableView!, numberOfRowsInSection section: Int) -> Int {
        return 10
    }
    
    
    func tableView(tableView: UITableView!, cellForRowAtIndexPath indexPath: NSIndexPath!) -> UITableViewCell! {
        let cell: UITableViewCell = UITableViewCell(style: UITableViewCellStyle.Subtitle, reuseIdentifier: "MyTestCell")
        
        cell.text = "Row #\(indexPath.row)"
        cell.detailTextLabel.text = "Subtitle #\(indexPath.row)"
        
        return cell
    }
 
 
}
```
