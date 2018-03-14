# Lab05_504Code
See Below for code used to develop apps. 
## Part 1. Simple Map App Showing User Location With Custom Text, Subtext, and zoom.

### Discussion:
I worked off of one of the macbooks for this lab. I was able to create recreate some of the functionality demonstrated in the class room while adding some additional code snippets. I found this video as a great <a href="https://youtu.be/wU1XN-Gk1LM" > reference :</a>
```
ViewController.swift
SimpleMapApp

Created by Patrick on 3/11/18.
Copyright © 2018 UWT. All rights reserved.

import UIKit
import MapKit
import CoreLocation
class ViewController: UIViewController, MKMapViewDelegate {

    @IBOutlet weak var SimpleMap: MKMapView!
    
    let locationManager = CLLocationManager()
    
    override func viewDidLoad() {
        super.viewDidLoad()
      
        
        //Create Location for app to begin with
        var location = CLLocationCoordinate2DMake(
            44.827745,
            -92.943822)
        
    //Code block here establishes initial zoom of map app
        //Creates the level of zoom. Lower numbers increase zoom level (i.e. .00002)
        var span = MKCoordinateSpanMake(0.02, 0.02)
        //Defines the regional view, uses parameters previously established
        var region = MKCoordinateRegion(center: location, span: span)
        //sets region to the initial map app created
        SimpleMap.setRegion(region, animated: true)
        
    //Annnotation Variable and associated settings
        var annotation = MKPointAnnotation()
        //Calls previous variable containg location information
        annotation.coordinate = location
        //Established the dipslayed text
        annotation.title = "Cottage Grove, Mn"
        //Creates a subtitle text
        annotation.subtitle = "My Hometown"
        //Adds annotations to the map
        SimpleMap.addAnnotation(annotation)
    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
```
Here a snap shot of the app: 

<img src="images/504part1Screenshot.png" width = 200></img>

## Part II. Adding more functionality: Search Bar, Automatic Zoom and Annotation Creation

### Discussion:
For my second mapapp, I remained with Xcode and attempted to explore more functionality. I chose to remain with XCODE becuase I thought it would be great to continue on from the last point app that I created. I found this to be as straight forward as the previous applicaiton. I used a different vlogger,<a href="https://youtu.be/GYzNsVFyDrU"> the Swift Guy </a>, whose videos were also very good and detailed despite a few issues between Xcode/Swift versions. 

### Problems:
I used my 2012 iMac to complete this app. I am not if this is the reason I was having trouble. The intent of the applicaton wat to create a search bar that allowed users to search or locations. When I would test the Apple App in the emulator by clicking the<b> search button </b>, the application would freeze. This did not allow me to get another picture of an actual customized location. In the background of the picture below is the resulting error code that was generated when I attempted to enter a location. 

I also tried to call a different map background but it would not work. I followed the steps <a href= "https://www.mapbox.com/install/"></a>. It kept saying that there was no module named MapBox

```
//  ViewController.swift
//  testNavContorller
//
//  Created by Patrick on 3/12/18.
//  Copyright © 2018 UWT. All rights reserved.
//

import UIKit
import MapKit
class ViewController: UIViewController, UISearchBarDelegate{
    
    
    @IBOutlet weak var MyMapView: MKMapView!
    @IBAction func SearchButton(_ sender: Any) {
        
        let searchController = UISearchController(searchResultsController: nil)
        searchController.searchBar.delegate = self
        present(searchController, animated: true, completion: nil)
    }
    func searchBarSearchButtonClicked(_ searchBar: UISearchBar)
    {
        //Ignore user
        UIApplication.shared.beginIgnoringInteractionEvents()

        //Activity Indeicator
        let activityIndicator = UIActivityIndicatorView()
        activityIndicator.activityIndicatorViewStyle = UIActivityIndicatorViewStyle.gray
        activityIndicator.center = self.view.center
        activityIndicator.hidesWhenStopped = true
        activityIndicator.startAnimating()
        
        self.view.addSubview(activityIndicator)
        //Hide Search bar
        searchBar.resignFirstResponder()
        dismiss(animated: true, completion: nil)
        
        //Create Search Request
        let searchRequest = MKLocalSearchRequest()
        searchRequest.naturalLanguageQuery = searchBar.text
        
         let activeSearch = MKLocalSearch(request: searchRequest)
        activeSearch.start {(response, error) in
            activityIndicator.stopAnimating()
            UIApplication.shared.endIgnoringInteractionEvents()
            if response == nil
            {
                print("Error")
            }
            else
            {
                //Remove annotations
                let annotations = self.MyMapView.annotations
                self.MyMapView.removeAnnotations(annotations)
                
                //Getting Data
                let latitude = response?.boundingRegion.center.latitude
                let longitude = response?.boundingRegion.center.longitude
                
                //create annotation
                let annotation = MKPointAnnotation()
                annotation.title = searchBar.text
                annotation.coordinate = CLLocationCoordinate2DMake(latitude!, longitude!)
                self.MyMapView.addAnnotation(annotation)
                
                // Zoom in on annotations
                let coordinate:CLLocationCoordinate2D = CLLocationCoordinate2DMake(latitude!, longitude!)
                let span = MKCoordinateSpanMake(0.1,0.1)
                let region = MKCoordinateRegionMake(coordinate, span)
                self.MyMapView.setRegion(region, animated: true)
            }
        }
    }
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view, typically from a nib.
    }
    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
}
```
Here is a snapshot:

<img src= "images/part2.png" width= 500></img>

## Update:
Turns out the old iMAC was the problem. See picture below for updated map app allowing the user to access a <b>search bar</b>, recenter the map, adjust zoom, and display annotation.

<img src= "images/GuamLocation.png" width= 200></img>

## Part III: Android Attempt. Simple Map application
### Discussion: 
This was probably the most overwhelming IDE. I think this was because we had all previously worked with XCODE more. Once I was able to get to a testing phase (visualization) I ran into issues. 
### Problems: 
I had issues setting up the emulator through the AVD. I tried multiple fixes <a href="https://stackoverflow.com/questions/41290134/android-studio-avd-manager-button-is-disabled">listed at StackOverflow </a> : Run as Administrator, Deleting .idea folder, and reinstallation (x2). The picture below shows the a grayed-out AVD (emulator set up). Without this I was unable to view my applcation. 

Here is a snapshot:

<img src= "images/AVD_Pic.png" width= 500></img>
