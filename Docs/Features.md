# RippleGL Features Documentation

## Overview

RippleGL is a browser-based ripple tank simulation that demonstrates wave physics, interference patterns, and acoustic phenomena. Originally written by Paul Falstad as a Java applet, it has been ported to run in modern browsers using GWT (Google Web Toolkit) and WebGL for high-performance real-time simulation.

**Live Demo:** http://www.falstad.com/ripple/

## Core Simulation Features

### Wave Physics Simulation
- Real-time wave propagation using WebGL shaders
- Support for both electromagnetic and acoustic wave modes
- Accurate wave interference and superposition
- Reflection, refraction, and diffraction effects
- Variable wave speed and damping

**Implementation Files:**
- `src/com/falstad/ripple/client/RippleSim.java` - Main simulation engine
- `war/Ripple.html` - WebGL shaders for wave simulation and rendering

### Wave Sources

#### Point Source (`Source.java`)
- **Description:** Basic point wave source with configurable frequency and amplitude
- **Properties:**
  - Frequency (adjustable via frequency slider)
  - Waveform: Sine, Square, Pulse, Triangle
  - Phase shift
  - Strength/amplitude
  - Enabled/disabled state
- **Files:** `src/com/falstad/ripple/client/Source.java`

#### Line Source (`LineSource.java`)
- **Description:** Extended linear wave source
- **Properties:** Inherits from Source with line geometry
- **Files:** `src/com/falstad/ripple/client/LineSource.java`

#### Moving Source (`MovingSource.java`)
- **Description:** Point source that moves, demonstrating Doppler effect
- **Properties:** All Source properties plus velocity and path
- **Files:** `src/com/falstad/ripple/client/MovingSource.java`

#### Multipole Source (`MultipoleSource.java`)
- **Description:** Source with multiple poles for complex radiation patterns
- **Subtypes:**
  - Dipole (2 poles)
  - Quadrupole (4 poles)
  - Hexapole (6 poles)
  - Octupole (8 poles)
  - 12-pole
- **Files:** `src/com/falstad/ripple/client/MultipoleSource.java`

#### Rotating Source (`RotatingSource.java`)
- **Description:** Multipole source that rotates
- **Properties:** Multipole properties plus rotation speed
- **Files:** `src/com/falstad/ripple/client/RotatingSource.java`

#### Phased Array Source (`PhasedArraySource.java`)
- **Description:** Array of sources with controllable phase relationships
- **Applications:** Beam steering and focusing
- **Files:** `src/com/falstad/ripple/client/PhasedArraySource.java`

### Physical Objects and Boundaries

#### Walls (`Wall.java`)
- **Description:** Reflective barriers that block wave propagation
- **Properties:**
  - Start and end points (draggable handles)
  - Reflection coefficient
- **Files:** `src/com/falstad/ripple/client/Wall.java`

#### Moving Walls (`MovingWall.java`)
- **Description:** Walls that move during simulation
- **Applications:** Doppler effect demonstrations
- **Files:** `src/com/falstad/ripple/client/MovingWall.java`

#### Slits (`Slit.java`)
- **Description:** Openings in walls for diffraction experiments
- **Applications:** Single slit, double slit, triple slit diffraction
- **Files:** `src/com/falstad/ripple/client/Slit.java`

#### Boxes and Barriers
- **SolidBox** (`SolidBox.java`): Rectangular solid barriers
- **Box** (`Box.java`): Basic rectangular objects
- **Cavity** (`Cavity.java`): Resonant chambers for standing wave modes
- **WindowBox** (`WindowBox.java`): Boxes with openings

### Medium Properties

#### Medium Boxes (`MediumBox.java`)
- **Description:** Rectangular regions with different wave properties
- **Properties:**
  - Wave speed (refractive index)
  - Boundary behavior
- **Applications:** Refraction, slow/fast medium demonstrations
- **Files:** `src/com/falstad/ripple/client/MediumBox.java`

#### Medium Ellipse (`MediumEllipse.java`)
- **Description:** Elliptical regions with different wave properties
- **Files:** `src/com/falstad/ripple/client/MediumEllipse.java`

#### Gradient Box (`GradientBox.java`)
- **Description:** Regions with spatially varying wave speed
- **Applications:** Temperature gradients, atmospheric effects
- **Files:** `src/com/falstad/ripple/client/GradientBox.java`

### Optical Elements

#### Lenses (`Lens.java`)
- **Description:** Focusing elements that bend wave paths
- **Types:**
  - Planar convex lens
  - Biconvex lens
- **Files:** `src/com/falstad/ripple/client/Lens.java`

#### Prisms
- **Parabolic Reflectors** (`Parabola.java`): Parabolic focusing mirrors
- **Triangle Prism** (`TrianglePrism.java`): Triangular prisms for refraction
- **Files:** 
  - `src/com/falstad/ripple/client/Parabola.java`
  - `src/com/falstad/ripple/client/TrianglePrism.java`

### Measurement Tools

#### Probes (`Probe.java`)
- **Description:** Point sensors for measuring wave amplitude
- **Features:**
  - Real-time amplitude display
  - Phase measurement
- **Files:** `src/com/falstad/ripple/client/Probe.java`

#### Probe View (`ProbeView.java`)
- **Description:** Display panel for probe measurements
- **Files:** `src/com/falstad/ripple/client/ProbeView.java`

## Control Interface

### Main Controls

#### Simulation Control
- **Run/Stop Button** (`stoppedCheck`): Pause/resume simulation
- **Speed Slider** (`speedBar`): Control simulation speed
- **Reset Button**: Clear all waves and restart

#### Wave Parameters
- **Frequency Slider** (`freqBar`): Adjust source frequency (0.01 - 2.0 Hz)
- **Damping Slider** (`dampingBar`): Control wave attenuation (0.0 - 1.0)
- **Brightness Slider** (`brightnessBar`): Adjust display brightness

#### Display Options
- **3D View Toggle** (`view3dCheck`): Switch between 2D and 3D visualization
- **Color Scheme Chooser** (`colorChooser`): Select color palette
- **Resolution Slider** (`resBar`): Adjust simulation grid resolution

### Visual Settings

#### Color Schemes (`schemeColors`)
Multiple predefined color schemes for:
- Wall color
- Positive wave amplitude
- Negative wave amplitude  
- Zero amplitude (neutral)
- Medium regions
- Wave sources

#### Wave Display Options
- **Waveform Type** (`waveChooser`): Visual representation mode
- **Mode Selection** (`modeChooser`): Different display modes

**Implementation Files:**
- Color handling: `src/com/falstad/ripple/client/Color.java`
- UI controls: Various files in `src/com/falstad/ripple/client/`

## Examples and Presets

### Built-in Examples (75+ presets)
Located in `src/com/falstad/ripple/public/examples/` with index in `setuplist.txt`:

#### Basic Wave Phenomena
- **Single Source** (`1source.txt`): Basic point source
- **Two Sources** (`2sources.txt`): Interference patterns
- **Four Sources** (`4sources.txt`): Complex interference
- **Plane Wave** (`plane.txt`): Uniform wave fronts
- **Intersecting Planes** (`interplane.txt`): Plane wave interference

#### Diffraction and Interference
- **Single Slit** (`1slit.txt`): Single slit diffraction
- **Double Slit** (`2slit.txt`): Classic interference experiment
- **Triple Slit** (`3slit.txt`): Multiple slit patterns
- **Obstacle** (`obstacle.txt`): Scattering around objects

#### Doppler and Motion Effects
- **Doppler Effect 1** (`doppler1.txt`): Moving source
- **Doppler Effect 2** (`doppler2.txt`): Alternative configuration
- **Sonic Boom** (`sonicboom.txt`): Supersonic source
- **Rotating Source** (`rotating.txt`): Rotating multipole

#### Resonance and Standing Waves
- **Big 1x1 Mode** (`bigmode.txt`): Fundamental cavity mode
- **1x1 Modes** (`11modes.txt`): Basic cavity resonance
- **1xN Modes** (`1nmodes.txt`): Higher order modes
- **NxN Modes** (`nnmodes.txt`): 2D cavity modes
- **Coupled Cavities** (`coupledcav.txt`): Resonator coupling
- **Room Resonance** (`roomres.txt`): Acoustic room modes

#### Optical Elements
- **Anti-Reflective Coating** (`coating.txt`): Interference coating
- **Zone Plate (Even)** (`zonee.txt`): Fresnel zone plate
- **Zone Plate (Odd)** (`zoneo.txt`): Alternative zone plate
- **Planar Convex Lens** (`plens.txt`): Simple lens
- **Biconvex Lens** (`blens.txt`): Double convex lens
- **Parabolic Mirror** (`paramirror1.txt`, `paramirror2.txt`): Focusing mirrors

#### Waveguides and Filters
- **Waveguides 1-5** (`waveguides1.txt` through `waveguides5.txt`): Various guide geometries
- **Low-Pass Filter** (`lowpass1.txt`, `lowpass2.txt`): Frequency filtering
- **High-Pass Filter** (`highpass1.txt`, `highpass2.txt`): High frequency transmission
- **Band-Stop Filter** (`bandstop1.txt` through `bandstop3.txt`): Notch filters

#### Advanced Phenomena
- **Temperature Gradients** (`gradient1.txt` through `gradient4.txt`): Variable medium
- **Reciprocity** (`reciprocity.txt`): Wave reciprocity theorem
- **Lloyd's Mirror** (`lloyd.txt`): Interference with reflection
- **Scattering** (`scatter.txt`): Multiple scattering effects

## Data Import/Export

### File Formats
- **Setup Files**: Text format with object definitions
- **URL Export**: Share configurations via URL parameters
- **Local File Export**: Save/load from local files

### Import/Export Dialogs
- **ImportFromTextDialog** (`ImportFromTextDialog.java`): Load from text
- **ExportAsUrlDialog** (`ExportAsUrlDialog.java`): Generate shareable URLs
- **ExportAsTextDialog** (`ExportAsTextDialog.java`): Save as text
- **ExportAsLocalFileDialog** (`ExportAsLocalFileDialog.java`): Local file operations

**Implementation Files:**
- `src/com/falstad/ripple/client/ImportFromTextDialog.java`
- `src/com/falstad/ripple/client/ExportAs*.java`

## URL Parameters

### Startup Configuration
The application supports URL parameters for initial setup:

```
Ripple.html?startExample=<filename>     # Load specific example
Ripple.html?rol=<string>                # Load from URL
Ripple.html?colorScheme=rrggbb,rrggbb,... # Custom colors (8 hex values)
```

**Implementation:** `src/com/falstad/ripple/client/QueryParameters.java`

## Build and Deployment

### Build System
- **Technology**: Google Web Toolkit (GWT) 2.7.0
- **IDE**: Eclipse with GWT plugin
- **Output**: JavaScript web application

### Build Files
- **GWT Module**: `src/com/falstad/ripple/Ripple.gwt.xml`
- **Entry Point**: `src/com/falstad/ripple/client/Applets.java`
- **Web Config**: `war/WEB-INF/web.xml`

### Deployment Targets
1. **Web Application**: Deploy `war/` directory contents to web server
2. **Electron App**: Desktop application using `app/` directory files

### Electron Configuration
- **package.json**: `app/package.json`
- **Main Process**: `app/main.js`
- **Renderer**: `app/renderer.js`
- **Preload Script**: `app/preload.js`

## Technical Architecture

### Core Classes
- **RippleSim**: Main application class and simulation engine
- **DragObject**: Base class for interactive objects
- **RectDragObject**: Base for rectangular objects
- **EditDialog**: Property editing interface
- **Setup**: Configuration management

### WebGL Implementation
- **Simulation Shader**: `shader-simulate-fs` - Wave physics computation
- **Display Shader**: `shader-display-fs` - Wave visualization
- **3D Shader**: `shader-3d-vs` - 3D surface rendering
- **Utility Shaders**: Various specialized rendering shaders

### Libraries and Dependencies
- **WebGL Utils**: `war/webgl-utils.js`
- **glMatrix**: `war/glMatrix-0.9.5.min.js` - Matrix operations
- **GWT**: Google Web Toolkit framework

## Performance Features

### Optimization
- **WebGL Acceleration**: GPU-based wave simulation
- **Variable Resolution**: Adjustable grid size for performance
- **Efficient Rendering**: Shader-based visualization
- **Frame Rate Control**: Adjustable simulation speed

### Browser Compatibility
- **Modern Browsers**: Chrome, Firefox, Safari, Edge
- **WebGL Required**: Hardware acceleration needed
- **Mobile Support**: Touch interface for tablets

## License and Credits

- **License**: GNU General Public License v2+
- **Original Author**: Paul Falstad
- **GWT Port**: Based on CircuitJS1 adaptation by Iain Sharp
- **Electron Support**: Contributed by @Immortalin

**License File**: See repository root for full GPL license text.

## File Structure Summary

```
ripplegl_fork/
├── README.md                    # Main documentation
├── Docs/
│   └── Features.md             # This feature documentation
├── src/com/falstad/ripple/
│   ├── Ripple.gwt.xml          # GWT module configuration
│   ├── client/                 # Main application source
│   │   ├── RippleSim.java      # Core simulation engine
│   │   ├── Source.java         # Wave source base class
│   │   ├── Wall.java           # Reflective barriers
│   │   ├── MediumBox.java      # Variable medium regions
│   │   └── [50+ other classes] # Object types and UI
│   └── public/
│       ├── setuplist.txt       # Example index
│       └── examples/           # 75+ example configurations
├── war/                        # Web application files
│   ├── Ripple.html            # Main HTML with WebGL shaders
│   ├── Ripple.css             # Styling
│   └── [generated files]      # GWT compilation output
└── app/                        # Electron application files
    ├── package.json           # Node.js configuration
    ├── main.js               # Electron main process
    └── [support files]       # Electron-specific code
```

This documentation covers all major features, settings, and implementation details of the RippleGL application. Each feature is linked to its corresponding source files for developers who want to understand or modify the implementation.