# google-map-direction-geolocation
A javascript sample code for plotting direction from user's current location to their destination



# This javascript code simply fetches the user's current location (latitude and longitude) as the origin, then accepts
a text address as the destination. That's what makes this code useful. 

## Write this CSS code for the map. Note that if there is no width and height, sorry your evil map will not work and it will not tell you why 
````
<style>
      /* Always set the map height explicitly to define the size of the div
       * element that contains the map. */
      #map {
        height: 400px;
        width: 100%;
      }
      /* Optional: Makes the sample page fill the window. */
      html, body {
        height: 100%;
        margin: 0;
        padding: 0;
      }
 
    </style> 
````

## Inside this HTML anywhere in your page where you want the map to show 
   `
    <div id="map"></div>
    `
    
    
## The below is just an element holding the destination, I have it hidden. You can unhide yours. 
   
    <input type="hidden" value="Empire state building, new york city" id="end" />
  

## Below is the javascript, please read the instruction in the last 3 lines of the javascript 

````
<script>

      function initMap() {

              // Try HTML5 geolocation.
     if (navigator.geolocation) {
            
            navigator.geolocation.getCurrentPosition(function(position) {
                var pos = {
                lat: position.coords.latitude,
                lng: position.coords.longitude
                };

                window.pos = pos; 


        var directionsService = new google.maps.DirectionsService;
        var directionsDisplay = new google.maps.DirectionsRenderer;
      //  ourOrigin = new google.maps.LatLng(pos.lat, pos.lng);
        var map = new google.maps.Map(document.getElementById('map'), {
          zoom: 7,
          center: {lat: pos.lat, lng: pos.lng}
        });
        directionsDisplay.setMap(map);

          calculateAndDisplayRoute(directionsService, directionsDisplay);


            });
            } else {
            // Browser doesn't support Geolocation
            handleLocationError(false, infoWindow, map.getCenter());
            }



        
       }

      function calculateAndDisplayRoute(directionsService, directionsDisplay) {

          console.log("Testing : "+pos);

        directionsService.route({
          origin:  new google.maps.LatLng(pos.lat, pos.lng),
          destination: document.getElementById('end').value,
          travelMode: 'DRIVING'
        }, function(response, status) {
          if (status === 'OK') {
            directionsDisplay.setDirections(response);
          } else {
            window.alert('Directions request failed due to ' + status);
          }
        });
      }
    </script>
    
    <script async defer
    src="https://maps.googleapis.com/maps/api/js?key=GOOGLE-MAP-DIRECTION-API-KEY&callback=initMap">
    
    //you need to enable google map, and google direction javascript APIs from inside your http://console.developers.google.com account
//You then have to insert the key in place of the GOOGLE-MAP-DIRECTION-API-KEY above.
    </script>
````


## Thank me
If this code saved your life, check me out on udemy.com/users/daveozoalor
