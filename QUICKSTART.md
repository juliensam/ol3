OpenLayers 3 Quick Start
========================

Some text to introduce this document and the library...


Getting the library
-------------------

How to get the library


First steps
-----------

To include a map a web page you will need 3 things:

 1. Include OpenLayers
 2. `<div>` map container
 3. JavaScript to create a simple map


Here is a really simple example:


    <!doctype html>
    <html lang="en">
      <head>
        <style>
          .map {
            height: 400px;
            width: 100%;
          }
        </style>
        <script src="http://ol3js.org/en/master/build/ol.js" type="text/javascript"></script>

        <title>OpenLayers 3 example</title>
      </head>
      <body>
        <div id="map" class="map"></div>
        <h4 id="title">OpenLayers example</h4>

        <script type="text/javascript">
          var map = new ol.Map({
            target: 'map',
            layers: [
              new ol.layer.Tile({
                source: new ol.source.MapQuestOpenAerial()
              })
            ],
            view: new ol.View2D({
              center: ol.proj.transform([37.40570, 8.81566], 'EPSG:4326', 'EPSG:3857'),
              zoom: 4
            })
          });
        </script>

      </body>
    </html>


#### Include OpenLayers

    <script src="http://ol3js.org/en/master/build/ol.js" type="text/javascript"></script>

The first part is to include the JavaScript library. For the purpose of this tutorial, here we simply point to the ol3js.org website to get the whole library. In a production environment, we would build a custom version of the library including only the module needed for our application.


#### `<div>` to contain the map

    <div id="map" class="map"></div>

The map in the application is contained in a [`<div>` HTML element](http://en.wikipedia.org/wiki/Span_and_div). Through this `<div>` the map properties like width, height and border can be controlled through CSS. Here's the CSS element used to make the map 400 pixels high and as wide as the browser window.

    <style>
      .map {
        height: 400px;
        width: 100%;
      }
    </style>


#### JavaScript to create a simple map

    var map = new ol.Map({
      layers: [
        new ol.layer.Tile({
          source: new ol.source.MapQuestOpenAerial()
        })
      ],
      target: 'map',
      view: new ol.View2D({
        center: ol.proj.transform([37.40570, 8.81566], 'EPSG:4326', 'EPSG:3857'),
        zoom: 4
      })
    });

With this JavaScript code, a map object is created with a MapQuest Open Aerial layer zoomed on the African East coast. Let's break this down:

The following line creates an OpenLayers `Map` object. Just by itself, this does nothing since there's no layers or interaction attached to it.

    var map = new ol.Map({ ... });

To attach the map object to the `<div>`, the map object takes a `target` into arguments. The value is the `id` of the `<div>`:

            target: 'map',


The `layers: [ ... ]` array is used to define the list of layers available in the map. The first and only layer right now is a tiled layer:

      layers: [
        new ol.layer.Tile({
          source: new ol.source.MapQuestOpenAerial()
        })
      ]

Layers in OpenLayers 3 are defined with a type (Image, Tile or Vector) which contains a source. The source is the protocol used to get the map tiles. You can consult the list of [available layer sources here](http://ol3js.org/en/master/apidoc/ol.source.html)

The next part of the `Map` object is the `View`. The view allow to specify the center, resolution, and rotation of the map. Right now, only `View2D` is supported, but other views should be available at some point. The simplest way to define a view is to define a center point and a zoom level. Note that zoom level 0 is zoomed out.

            view: new ol.View2D({
              center: ol.proj.transform([37.40570, 8.81566], 'EPSG:4326', 'EPSG:3857'),
              zoom: 4
            })

You will notice that the `center` specified is in lat/lon coordinates (EPSG:4326). Since the only layer we use is in Spherical Mercator projection (EPSG:3857), we can reproject them on the fly to be able to zoom the map on the right coordinates.