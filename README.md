# Flight-Tracker-Clock

A wall-mounted LED matrix display that shows real-time aircraft flying near your location.  
FlightWall will use ADS-B data from OpenSky and enriched flight metadata from FlightAware AeroAPI to display aircraft position, route, airline, and aircraft type on a modular 16×16 LED matrix wall — while also functioning as a large ambient clock when no aircraft are nearby.

![Main Concept](Images/Main.png)

---


##  Hardware Design

### Front (LED Matrix Layout)

![Front CAD](Images/Front.png)

- 10× WS2812B 16×16 LED matrices
- Seamless tiled display area
---

### Back (Electronics & Mounting)

![Back CAD](Images/Back.png)

- ESP32 controller
- Power distribution bus
- Level shifter
- Wall mounting points
---
##  Wireing
The panels will be wiered in a snake pattern like showns in this image
![DIN_DOUT](Images/wire_panel.png)

All other electronics wiring diagram
![Diagram](Images/wire.png)


##  Data Sources

FlightWall combines two aviation data sources:

### OpenSky Network
Provides live ADS-B state vectors:
- Latitude
- Longitude
- Altitude
- Heading
- ICAO24 identifier

Used for:
- Detecting aircraft within radius
- Real-time positioning on display

### FlightAware AeroAPI
Provides enriched metadata:
- Flight number
- Airline
- Origin / destination airports
- Aircraft type
- Airline name

Used for:
- Display info panel
- Airline identification
- Aircraft details

---


