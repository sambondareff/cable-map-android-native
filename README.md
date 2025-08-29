# Cable Map Android Native App

An interactive Android application displaying an SVG cable map with animated route overlays, placenames, and markers. The app features responsive scaling, smooth animations, and a clean user interface optimized for mobile devices.

## Features

- **Interactive SVG Map**: High-resolution cable map with proper viewport scaling
- **Animated Routes**: Individual route animations with GSAP-powered path drawing
- **Show All Routes**: Display all routes simultaneously with staggered animations
- **Route Markers**: SVG markers appear at route endpoints after animations complete
- **Placenames**: Scalable place name overlays positioned accurately on the map
- **Responsive Design**: Optimized for various Android screen sizes and orientations
- **Bottom Navigation**: Route selection menu positioned in bottom-left corner for better mobile UX

## Technical Implementation

### Architecture
- **Native Android**: Built with Android SDK and WebView
- **WebView Bridge**: AndroidAssets bridge for loading local SVG and JSON files
- **Viewport Scaling**: Unified scaling approach preventing clipping on any screen size
- **Asset Management**: All interactive content loaded from `assets/` directory

### Key Technologies
- **Android SDK**: Native Android application framework
- **WebView**: Renders HTML/CSS/JavaScript content
- **GSAP**: Green Sock Animation Platform for smooth route animations
- **SVG**: Scalable Vector Graphics for map and route content
- **JSON**: Route metadata and positioning data

### Scaling System
The app uses a unified viewport scaling approach:

1. **Base Map**: Stretches to fill entire viewport using `100vw × 100vh`
2. **Route Overlays**: Use viewport stretching with `viewBox="0 0 2944 1840"` and `preserveAspectRatio="none"`
3. **Placenames**: Scaled positions using `scaleFactorX = window.innerWidth / 2944`
4. **Markers**: Both position and content scaled to match map scaling
5. **Consistent Scaling**: All elements use same scaling factors for perfect alignment

## Project Structure

```
cable-map-android-native/
├── app/
│   ├── src/main/
│   │   ├── assets/
│   │   │   ├── cable-map.html          # Main WebView content
│   │   │   ├── gsap.min.js            # Animation library
│   │   │   ├── interactive/           # SVG files and interactive content
│   │   │   ├── placename-coordinates.json  # Placename positioning data
│   │   │   ├── route-coordinates-updated.json  # Route positioning data
│   │   │   └── route-markers.json     # Marker positioning data
│   │   ├── java/com/cablemap/
│   │   │   └── MainActivity.java      # Main Android activity
│   │   └── res/                       # Android resources
│   ├── build.gradle                   # App-level build configuration
│   └── proguard-rules.pro            # ProGuard configuration
├── gradle/                           # Gradle wrapper files
├── build.gradle                      # Project-level build configuration
├── settings.gradle                   # Project settings
└── README.md                         # This file
```

## Assets Overview

### JSON Data Files
- **`route-coordinates-updated.json`**: Contains positioning data and labels for individual routes
- **`placename-coordinates.json`**: Coordinates for placename overlay positioning
- **`route-markers.json`**: Marker positioning data for route endpoints

### Interactive Directory
- **`Base-Map.svg`**: Main cable map background
- **`placename-all.svg`**: Complete placename layer
- **Route SVGs**: Individual route path files
- **Marker SVGs**: Route endpoint marker graphics
- **Placename SVGs**: Individual placename overlay files

## Building the App

### Prerequisites
- Android SDK (API level 21+)
- Android Studio or Gradle command line tools
- Java 8+ or OpenJDK

### Build Instructions

1. **Clone/Download the project**
2. **Open in Android Studio** or navigate to project directory
3. **Build APK**:
   ```bash
   ./gradlew assembleDebug
   ```
4. **Install APK**:
   ```bash
   adb install app/build/outputs/apk/debug/app-debug.apk
   ```

### Build Variants
- **Debug**: Development build with debugging enabled
- **Release**: Production build (requires signing configuration)

## Installation

1. Enable "Unknown Sources" in Android Settings → Security
2. Install the APK file on your Android device
3. Launch the "Cable Map" app

## Usage

### Navigation
- **Route Buttons**: Located in bottom-left corner for easy thumb access
- **Individual Routes**: Tap any route button to animate that specific route
- **Show All Routes**: Display all routes simultaneously with color coding
- **Clear Route**: Remove currently displayed routes and markers

### Features
- **Route Animation**: Routes draw progressively using path animation
- **Markers**: Appear after route animation completes
- **Responsive**: Automatically adapts to screen size and orientation
- **Smooth Performance**: Optimized for mobile devices

## Development Notes

### WebView Configuration
- **JavaScript Enabled**: Required for interactive functionality  
- **DOM Storage**: Enabled for local data persistence
- **Initial Scale**: Set to 100% to delegate scaling to JavaScript
- **Wide Viewport**: Disabled to prevent conflicts with custom scaling

### Scaling Approach Evolution
The app went through several scaling iterations:
1. **Transform-based scaling** (clipping issues)
2. **Viewport stretching** (resolved clipping)
3. **Unified approach** (consistent scaling across all elements)

### Performance Optimizations
- **Asset Loading**: Local file loading via AndroidAssets bridge
- **Animation Library**: GSAP for smooth, hardware-accelerated animations
- **Viewport Scaling**: Efficient scaling without transform calculations
- **Memory Management**: Proper cleanup of route overlays

## Troubleshooting

### Common Issues
- **Routes not displaying**: Check asset loading in logcat
- **Scaling issues**: Verify viewport meta tag and scaling calculations
- **Animation problems**: Ensure GSAP library loads correctly
- **Marker positioning**: Check JSON coordinate data format

### Debug Information
The app logs detailed information to Android logcat:
- Viewport dimensions and scaling factors
- Asset loading status
- Animation progress
- Marker display confirmation

## Version History

### Current Version
- ✅ Unified viewport scaling approach
- ✅ Bottom-left menu positioning  
- ✅ Properly scaled markers
- ✅ Consistent route positioning
- ✅ No clipping on any screen size
- ✅ Smooth GSAP animations
- ✅ AndroidAssets bridge for local file loading

### Key Fixes Applied
1. **Viewport Scaling**: Implemented consistent scaling across all map elements
2. **Route Positioning**: Fixed alignment between individual and "Show All" routes
3. **Marker Scaling**: Applied proper scaling to both position and content
4. **Menu UX**: Moved controls to bottom-left for better mobile accessibility
5. **Asset Loading**: Corrected file loading paths and bridge configuration

## License

This project is intended for demonstration and educational purposes.

## Support

For technical issues or questions about the implementation, refer to the commit history and code comments for detailed information about the scaling system and WebView bridge configuration.
