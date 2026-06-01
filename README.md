# terrier-npm
### Terrier Visualization Toolkit Distribution

This is the NPM package repo for the Terrier toolkit.  Actual examples are on the [TerrierWeb repo](https://github.com/WetDogWeather/TerrierWeb).

Terrier is a weather visualization package for web and mobile.  This is the web version and the native version can be obtained from [Wet Dog Weather](https://wetdogweawther.com).

You'll need an API key to access Wet Dog Weather data.  [Contact us](https://wetdogweawther.com) for details.

### Documentation
Terrier will work with a variety of map toolkits, including MapLibre, Mapbox, ESRI Web SDK, Leaflet, and OpenLayers.  Consult our [TerrierWeb repo](https://github.com/WetDogWeather/TerrierWeb) for examples of each.  We'll include the MapLibre example here.

Set up and build your [MapLibre](https://github.com/maplibre/maplibre-native) web app as normal.
To add Terrier, you'll need to do the following.

Add the Terrier package.

    npm install @WetDogWeather/Terrier

In your map JS (or TS) file you'll need to import Terrier.

    import Terrier from '@wetdogweather/terrier'

Once you've got a MapLibre map started, you can integrate Terrier with it and give it your stack name.  'prod' is our stack, but you can use it for testing.

    // Tell Terrier to hook itself into MapLibre
    Terrier.startMapLibre(stackName, apiKey, map, (ovl) => {
        // Now you can display a layer
    })

The 'map' referenced is from MapLibre. stackName and apiKey are provided by Wet Dog Weather.

Once that callback is called, you're good to create layers.  And you'll need that ovl object in any case.  Within that callback you can start and modify layers like so.

        // Kick off a temperature layer
        let tempLayer = ovl.startLayer('temperature', {
            opacity: 0.5,
        })

        // Animate the results because why not
        ovl.timePlay({period: 10.0})

And that's basically it.  Your layer names are things like 'temperature' and 'wind_uv' and whatever else you may have paid for.  Take a look at the [terrier docs](doc/Terrier.md) for the full functionality.

### Installation Details
Terrier consists of a Javascript interface in the main terrier.js file.  It's documented in the repo and easy to follow.  It also has a fairly incomprehensible Emscripten generated JS file and associated web assembly.  You won't need to interact with those, but they do need to be included in your own distribution.

We've made that work with vite and other package managers, but if that fails the simplest thing to do is include the files we distribute under the public folder in the Terrier distribution.
