# Geohashing Chat by Proximity

### Try it now: [Geohash Chat by Proximity][1]

To connect groups of two or more people by location, you will take lat/long values and reduce the resolution of accuracy, and by doing this you can expand the coverage of proximity.  You can use multiple resolutions at once or a fixed resolution.  

> Get Source Code: [GitHub Repository for Geo Chat by Proximity][2]

![Geohashing Chat Conversations based on Proximity Zoom Level][3]

## Basics of Geo Hashing

Next we'll cover some source code snippet for geo hashing lat/long coords. It is fairly simple to increase the radius of lat/long position by reducing the accuracy of the float values.  Using this you can expand the circle and collect a Lat/Long.

    // -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
    // Geo Hash
    // -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
    function geohash( coord, resolution ) {
        var rez = Math.pow( 10, resolution || 0 );
        return Math.floor(coord * rez) / rez;
    }

![Acquire Lat Long Chat Proximity Location][4]

## Geo Hashing Resolution "Zoom"

"Zoom" levels, basically several different cartesian grids with larger and smaller granularity.  Once a Geofencing event fires, you will publish to a set of channels corresponding with each zoom level.  Zoom levels are important as that is how we actually construct the link between Geofencing and PubNub.  Zoom level is the resolution/de-resolution of the Cartesian coordinates Lat/Long (think X,Y coord).  By reducing the resolution of the lat/long coord we can construct a channel name that hits 1 box of the grid.  Less resolution means larger the boxes and is required to determine a PubNub Channel that is associated.

    // Create Proximity Channel
    channel = geohash( pos.latitude, 0 ) + '' + geohash( pos.longitude, 0 );

This will create a very wide circle and generate a channel name used to connect.  Next connect to PubNub with this channel name.

    // Connect to Proximity Channel
    pubnub.subscribe({
         channel : channel,
         message : recieve,
         connect : ready,
        presence : presence
    });

![Acquired Latitude Longitude Chat Proximity Group][5]

## Geo Hashing with PubNub Conclusion

That's it! You simply reduce the resolution of a geo coordinate and use that as a channel name on PubNub.  Also check out the browser's `navigator.geolocation.getCurrentPosition(...)` method to acquire lat/long in a chrome/firefox/ie/opera/mobile/safari browser.

> Also checkout the [PubNub Connected Car Solution Kit][7]

![Geohashing Chat Conversations based on Proximity Nearby][6]


  [1]: http://stephenlb.github.io/geohash-chat-by-proximity/
  [2]: https://github.com/stephenlb/geohash-chat-by-proximity
  [3]: http://i.stack.imgur.com/tV9S7.jpg
  [4]: http://i.stack.imgur.com/LUAvv.png
  [5]: http://i.stack.imgur.com/GQD3n.png
  [6]: http://i.stack.imgur.com/u0uE0.png
  [7]: http://www.pubnub.com/developers/connected-car/
