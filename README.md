# Lab05_504Code
See Below for code used to develop apps. 
## Part 1. Simple Map App Showing User Location With Custom Text, Subtext, and zoom.
'''
//  ViewController.swift
//  SimpleMapApp
//
//  Created by Patrick on 3/11/18.
//  Copyright © 2018 UWT. All rights reserved.
//
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
}
'''
