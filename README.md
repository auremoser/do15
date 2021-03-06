# OLITA Digital Odyssey 2015: Consuming and Transforming Open Data - a hands-on tutorial
  
## Who are you?
I'm Mita Williams. I'm the UX librarian from the University of Windsor.  I am copystar on twitter.

## Where am I?
Good question. If I gave you directions here, I would tell you we are at 51 Dockside Dr, Toronto, ON M5A 1B6.  
  
But if I wanted to describe the location as a point on a map, I might describe the same location using latitude and longitude:  43° 38' 39.2706", -79° 21' 55.4508"  You would read the above as "43 degrees, 38 minutes and 39.2706 seconds, negative 79 degrees, 21 minutes and 55.4508 seconds".
  
While it’s interesting that we describe a place using units of time (https://en.wikipedia.org/wiki/Longitude_(book)), its also confusing and somewhat unwieldy. So let's describe the same place using longitude and longitude but using decimal degrees instead of minutes and seconds. There are a number of conversion tools available online to do this : 43.644242, -79.365403  
  
## What if I wanted to tell people where the 102 library branches the TPL are in the city? 
You could make a map using Google Maps of all the TPL Library branches: http://www.torontopubliclibrary.ca/hours-locations/  

## How could I make this map?
First you will need the locations of all 102 branches of the Toronto Public Library. These are provided by the City of Toronto from their Open Data Catalogue at: http://www1.toronto.ca/wps/portal/contentonly?vgnextoid=a7ae0ea14b661310VgnVCM1000003dd60f89RCRD&vgnextchannel=1a66e03bb8d1e310VgnVCM10000071d60f89RCRD  
  
These location files are in .kml which is a notation for XML that first made popular by Google Earth before becoming standardized. Google Mapping Products happily use kml files. Look at http://www.torontopubliclibrary.ca/data/library-data.kml to see how the locations are described:

```
<Placemark id="LIB02">
<name>Agincourt</name>
<description>
Address: 155 Bonis Ave., Toronto, ON, M1T 3W6<br/>Link: http://www.torontopubliclibrary.ca/detail.jsp?R=LIB02
</description>
<address>155 Bonis Ave., Toronto, ON, M1T 3W6</address>
<phoneNumber>416-396-8943</phoneNumber>
<Point>
<coordinates>-79.29342962962961,43.78516666666665</coordinates>
</Point>
</Placemark>
```

Notice that the point coordinates are in the format <coordinates>longitude, latitude</latitude>. Some geoformats are long, lat and others are long, lat. This makes everyone sad.   

Also note that the data in the catalogue is out of date. The site provides the location of Library Branch Locations (http://www.torontopubliclibrary.ca/data/library-data.kml) and Future Library Branch Locations (http://www.torontopubliclibrary.ca/data/new-library-data.kml) but all the future branches have now opened.  

I have already combined these files together into a new file called:   
https://github.com/copystar/do15/blob/master/combined-library-data.kml   
  
It's also available on drive at:   
https://drive.google.com/open?id=0B5RDRo0uB7m5SWFEbkVWSmdvdHc&authuser=0   
  
## Task 1: Make a map using the kml file provided
If you get stuck, please put a post-it note on your laptop
  
**Using Google Map**
- https://www.google.com/maps/d/
- create account if you don't already have a Gmail account
- click on *Import Map* in top left hand menu (or *My Maps* -> *Create map* in some Google Maps UIs)
- upload combined-library.data.kml
- explore changing the map features if you would like

**Using CartoDB**  
- https://cartodb.com/
- create account if you don't already have a CartoDB account
- click on *Create Map*; select *Map View* at the top of the screen
- click on the '+' or *Add Layer* option at the top of the right side menu
- upload combined-library.data.kml
- explore changing the map features if you would like
   
**Using Mapbox**
- https://mapbox.com/
- create account if you don't already have a Mapbox account
- click on the *Data* tab at the top right hand corner of the screen; click on import
- upload combined-library.data.kml
- select map features if you would like then click on Import Features
- explore changing the map features if you would like
    
## Bonus challenge: Using Leaflet and Openstreetmap tiles
If you are comfortable with HTML and JavaScript, try making a map from scratch using Leaflet.js (http://leafletjs.com/) to attach a set of points to a map made of tiles provided by OpenStreetMap.  
  
You will first need to convert your kml file into GeoJSON. GeoJSON is a file format that is easily digestable by JavaScript. There are many tools that can do this but for this exercise try http://geojson.io/   

- go to http://geojson.io/  
- from the menu *Open* select *File* and upload our kml file: https://github.com/copystar/do15/blob/master/combined-library-data.kml 
- notice how GeoJSON looks like in the side-menu


```
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [
          -79.26925185185183,
          43.708018518518514
        ]
      },
      "properties": {
        "name": "Albert Campbell",
        "description": "Address: 496 Birchmount Road, Toronto, ON, M1K 1N8<br/>Link: http://www.torontopubliclibrary.ca/detail.jsp?R=LIB03"
      }
    },
```
- after the map is drawn, from the menu *Save*, select *GeoJSON" 
- refer to "Adding GeoJSON to Leaflet with Link Relations" : http://lyzidiamond.com/posts/osgeo-august-meeting/ to find the HTML that use can use as a template that will import GeoJSON into a map created by Leaflet.js
- use *http://{s}.tile.osm.org/{z}/{x}/{y}.png* for your map tiles
- use tpl-branches.json for your geojson layer: https://github.com/copystar/do15/blob/master/tpl-branches.json  
- explore changing the map features if you would like using Leaflet.js http://leafletjs.com/
- refer to tpl-branches-leaflet-osm.html in this repo if you get stuck
 
## Task 2 : Add the dimension of time 
  
While our map of the Toronto Public Library branches is informative, it can become complex and interesting if we add more the year of establishment to each branch. Doing so will allow the reader to learn the rate of the TPL growth and where this growth occurred. We do have a problem though. The Open Data Catalogue from the City of Toronto does not provide this information.  
  
A list of TPL Branches that does include year of opening can be found on Wikipedia: https://en.wikipedia.org/wiki/List_of_Toronto_Public_Library_branches  but this table does not provide the addresses nor the geolocations of each branch.  

### Combine the kml file with the Wikipedia table of TPL branch opening dates using Google Fusion Tables

Google Fusion Tables is a Google product that adds visualization to structured data. Alternatively, these data tables could be combined using command-line tools or using services such as CartoDB.  

#### First we will import our combined-library.data.kml file

- https://sites.google.com/site/fusiontablestalks/home
- click on *Create a fusion table* from https://support.google.com/fusiontables/answer/2571232
- click on *Choose File* from the *Import New Table" pop-up screen; then click *next*
- import https://raw.githubusercontent.com/copystar/do15/master/combined-library-data.kml  
- it will ask you to confirm, *Column names are in row 1*, click *next*, change name if you'd like, then click *finish*
- notice that the *Map of Geometry* tab is a map of the 102 branches

#### Then we are going to add the Wikipedia Table to our kml file

### You can try to import the Wikipedia table into Google Fusion Tables...
- open the *File* menu and select *Find a table to merge with*
- a window with the heading, *Merge: Select a Table" should pop-up
- from 'Suggest tables matching on' dropdown menu, select 'name'
- select the table *List of Toronto Public Library branches - Wikipedia* in the list and then *next*
- you will be asked to confirm the match; click *next*
- select all fields to be merged; click *next*
- you should have a new merged table of both data tables
- go to the tab of the *Map of Geometry*
- from the File menu, select *Download* as kml

###... but if that doesn't work, import the Wikipedia table this way...
- open the *File* menu and select *Merge...*
- download and import the Wikipedia table found here: https://drive.google.com/open?id=1aRIFZ0fMJptaZf-tvUsL4ZI7_KurknKneJfjyQzl&authuser=0  
- you will be asked to confirm the match; click *next*
- select all fields to be merged; click *next*
- you should have a new merged table of both data tables
- go to the tab of the *Map of Geometry*
- from the File menu, select *Download* as kml
  
###... and if all else fails...
- use this file : https://drive.google.com/open?id=17rQmkQzoz3bAVA33-4HEJRfdlMkR4h0hwS8CANQf&authuser=0  
- go to the tab of the *Map of Geometry*
- from the File menu, select *Download* as kml

## Task 3 : Let's make a time map (again!) 

You should now have a downloaded kml file of the 102 branches that now includes the year of opening. If not, use this file https://github.com/copystar/do15/blob/master/Merge-of-TPL-Library-Branches-and-Wikipedia.kml  

We are now going to create an animation of this branch openings using Cartodb.com  

- https://cartodb.com/
- create account if you don't already have a CartoDB account
- click on *Create Map*; after the information screen, select *Connect Dataset* from the *Dataset* page
- select and upload upload Merge-of-TPL-Library-Branches-and-Wikipedia.kml
- click on green *Connect dataset* button at the bottom of the screen
- select *Data View* at the top of the screen
- under the *Built* column, mouse over the word *string*; then pull down the menu to select *number*; confirm the action
- select *Map View* at the top of the screen
- from the right hand menu, click on the paintbrush icon (wizards)
- from the list of visualizations, click on the right arrow until you see and select the option *Torque*
- from the next line, activate on the *Cumulative* switch
- from the next line, select *built* from the drop down menu for the *Time Column*
- an animation should begin in the main map screen
- explore changing the map features if you would like
 

Here be dragons.
