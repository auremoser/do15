# OLITA Digital Odyssey 2015: Consuming and Transforming Open Data - a hands-on tutorial
  
## Who are you?
I'm Mita Williams. I'm the UX librarian from the University of Windsor.  I am copystar on twitter.

## Where am I?
Good question. If I gave you directions here, I would tell you we are at 51 Dockside Dr, Toronto, ON M5A 1B6.  
  
But if I wanted to describe the location as a point on a map, I might describe the same location using latitude and longitude:  43° 38' 39.2706", -79° 21' 55.4508"  You would read the above as "43 degrees, 38 minutes and 39.2706 seconds, negative 79 degrees, 21 minutes and 55.4508 seconds".
  
While it’s interesting that we describe a place using units of time (https://en.wikipedia.org/wiki/Longitude_(book)), its also confusing and somewhat unweildy. So let's describe the same place using longitude and longitude but using decimal degrees instead of minutes and seconds. There are a number of conversion tools available online to do this : 43.644242, -79.365403  
  
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

Notice that the point coordinates are in the format <coordinates>longitude, latitude</latitude>. Some geoformats are long, lat and others are long, lat.   
  
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
- click on *Import Map* in top left hand menu
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
    
**Bonus challenge: Using Leaflet and Openstreetmap tiles**
- refer to "Adding GeoJSON to Leaflet with Link Relations" : http://lyzidiamond.com/posts/osgeo-august-meeting/
- use *http://{s}.tile.osm.org/{z}/{x}/{y}.png* for your map tiles
- use tpl-branches.json for your geojson layer: https://drive.google.com/open?id=0B5RDRo0uB7m5NHVvSWlBZTI3cHM&authuser=0  
- explore changing the map features if you would like
- refer to tpl-branches-leaflet-osm.html in this repo if you get stuck
 
## Task 2 : Add the dimension of time so we can make a time-map
  
While our map of the Toronto Public Library branches is informative, it can become complex and interesting if we add more the year of establishment to each branch. Doing so will allow the reader to learn the rate of the TPL growth and where this growth occurred. We do have a problem though. The Open Data Catalogue from the City of Toronto does not provide this information.  
  
A list of TPL Branches that does include year of opening can be found on Wikipedia: https://en.wikipedia.org/wiki/List_of_Toronto_Public_Library_branches  but this table does not provide the addresses nor the geolocations of each branch.  

### Combine the kml file with the Wikipedia table of TPL branch opening dates using Google Fusion Tables

Google Fusion Tables is a Google product that adds visualization to structured data. Alternatively, these data tables could be combined using command-line tools.  

- https://sites.google.com/site/fusiontablestalks/home
- click on *Create a fusion table* from https://support.google.com/fusiontables/answer/2571232
- click on *Choose File* from the *Import New Table" pop-up screen; then click *next*
- it will ask you to confirm, *Column names are in row 1*, click *next*, change name if you'd like, then click *finish*
- notice that the *Map of Geometry* tab is a map of the 102 branches

### You can try to import the Wikipedia table into Google Fusion Tables...
- open the *File* menu and select *Find a table to merge with*
- a window with the heading, *Merge: Select a Table" should pop-up
- from 'Suggest tables matching on' dropdown menu, select 'name'
- select the table *List of Toronto Public Library branches - Wikipedia* in the list and then *next*
- you will be asked to confirm the match; click *next*
- select all fields to be merged; click *next*
- you should have a new merged table of both data tables

###... but if that doesn't work, import the Wikipedia table this way...
- open the *File* menu and select *Merge...*
- download and import the Wikipedia table found here: https://www.google.com/fusiontables/data?docid=1purEYw-Cu-lN-sn_Kq_QqTzYCB5e3P0umXsgeSHl#rows:id=1
  
###... and if all else fails
- use this file 
 
