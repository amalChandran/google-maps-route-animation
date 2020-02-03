
<p align="left"><img src="extras/ic_app.png" width="15%" /></p>
<p align="left"><img src="extras/trail_logo.png" width="15%"/></p>
<p align="left">Smooth route animation over Google maps. Uses projection from Google maps to draw a route on an overlay layout. Can add multiple routes with different sytles while supporting pan and zoom of maps.</p>
<p align="left">
  <a href="https://travis-ci.org/amalChandran/trail-android/"><img src="https://travis-ci.org/amalChandran/trail-android.svg?branch=master" alt="Build Status"></a>
  <a href="https://android-arsenal.com/details/1/6435"> <img src="https://img.shields.io/badge/Android%20Arsenal-amal%20chandran-green.svg?style=flat" alt="Android Arsenal"></a>
  <a href="https://github.com/angular/angular.js/blob/master/LICENSE"><img src="https://img.shields.io/badge/License-MIT-lightgrey.svg" alt="License: MIT"></a>
</p>

<p align="left">
  (Gif running @ 10fps. Check the video on <a href="https://www.youtube.com/watch?v=ENOcDomhCPw">youtube</a>.)
</p>

| <img src="extras/trailv1.5.gif" width="200px;"/><br /><sub><b>Overlay polyline</b></sub><br/>        | <img src="extras/normalgif.gif" width="200px;"/><br /><sub><b>Marker and polyline</b></sub><br /> | <img src="extras/zoomGif.gif" width="200px;"/><br /><sub><b>With zoom</b></sub><br />                            | 
| :-----------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------: |

## Setup
1. Add jitpack to the root build.gradle file of your project at the end of repositories.
```
allprojects {
    repositories {
      ...
      maven { url 'https://jitpack.io' }
    }
}
```
2. Add the dependency
```
implementation 'com.github.amalChandran:trail-android:v1.51'
```
## Usage
Place RouteOverlayView over your google map layout in xml. Make sure that the routeoverlayview covers the map completely. This is the view in which the routes will be drawn.

```
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  xmlns:tools="http://schemas.android.com/tools"
  android:layout_width="match_parent"
  android:layout_height="match_parent">
  <fragment
    android:id="@+id/map"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:name="com.google.android.libraries.maps.SupportMapFragment"/>
  <com.amalbit.trail.RouteOverlayView
    android:id="@+id/mapOverlayView"
    android:layout_width="match_parent"
    android:layout_height="match_parent"/>
</FrameLayout>
```
In your activity, create routes with three predefined styles as of now.

```
googleMap.setOnMapLoadedCallback(() -> {
    Route normalOverlayPolyline = new Route.Builder(mRouteOverlayView)
        .setRouteType(RouteType.PATH)
        .setCameraPosition(mMap.getCameraPosition())
        .setProjection(mMap.getProjection())
        .setLatLngs(mRoute)
        .setBottomLayerColor(Color.YELLOW)
        .setTopLayerColor(Color.RED)
        .create();
```
To make sure that the overlay moves along with the Google maps movement we need to add a hook from its cameramovelistener.
```
googleMap.setOnCameraMoveListener(() -> {
      mRouteOverlayView.onCameraMove(googleMap.getProjection(), googleMap.getCameraPosition());
    }
);
```
Library uses java 8 bytecode, so dont forget to enable java 8 in your application's build.gradle file.
```
android {
    compileOptions {
        sourceCompatibility 1.8
        targetCompatibility 1.8
    }
}
```

## License
MIT © Amal Chandran

## Logo
<a href="https://dribbble.com/josephjrscribbles">Jibin Joseph</a>
