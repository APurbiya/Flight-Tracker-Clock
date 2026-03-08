# Flight-Tracker-Clock

A wall-mounted LED matrix display that shows real-time aircraft flying near your location.  
FlightWall will use ADS-B data from OpenSky and enriched flight metadata from FlightAware AeroAPI to display aircraft position, route, airline, and aircraft type on a modular 16×16 LED matrix wall — while also functioning as a large ambient clock when no aircraft are nearby.

![Main Concept](Images/Main.png)

---


##  Hardware Design
Onsape Link
https://cad.onshape.com/documents/5e10ae0c6bd23bd6d8d1bee4/w/9cd8f516c83d0d0f76abd4b4/e/88136dfb222c5cb764a34b15?renderMode=0&uiState=699baecf1584b8ae0255865d

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
##  Assembly
The way everything will be put together is simple, I am going to print the housing which has 10 cells each cell hold one of these [LED Matrix](https://www.aliexpress.us/item/2255800358269772.html?spm=a2g0o.cart.0.0.40a838dafTMLaR&mp=1&pdp_npi=6%40dis%21USD%21USD%20105.28%21USD%2056.85%21%21USD%2056.85%21%21%21%4021030a4b17730043375744252edfee%2112000032067904146%21ct%21US%216564620185%21%211%210%21&_gl=1*r6dhic*_gcl_au*MTA1MDMwNjU3NC4xNzcxMTcxMzM1*_ga*MTY3NjY4NDI5OC4xNzcyODM4ODc5*_ga_VED1YSGNC7*czE3NzMwMDQzMzkkbzIkZzAkdDE3NzMwMDQzMzkkajYwJGwwJGgw&gatewayAdapt=glo2usa) 10 of these together acts as my screen that will display all the flight info.
The back is simple going to screw onto the main frame using 4 m3 screws ot glue
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

  # Data and Software

## Data API Keys

The data for this project consists of two main data sources:
1. Core public [ADS-B](https://en.wikipedia.org/wiki/Automatic_Dependent_Surveillance%E2%80%93Broadcast) data for flight positions and callsigns - using [OpenSky](https://opensky-network.org)
2. Flight information lookup - aircraft, airline, and route (origin/destination airport). This is typically the hardest / most expensive information to find. Using [FlightAware AeroAPI](https://flightaware.com/aeroapi)

### Setting up OpenSky
1. Register for an [OpenSky](https://opensky-network.org/) account
2. Go to your [account page](https://opensky-network.org/my-opensky/account)
3. Create a new API client and copy the `client_id` and `client_secret` to the [APIConfiguration.h](firmware/config/APIConfiguration.h) file


### Setting up AeroAPI
1. Go to the [FlightAware AeroAPI]([https://flightaware.com/aeroapi](https://flightaware.com/aeroapi)) page and create a personal account
3. From the dashboard, open **API Keys**, click **Create API Key** and follow the steps
8. Copy the generated key and add it to [APIConfiguration.h](firmware/config/APIConfiguration.h)


## Software Setup

### Set your WiFi

Enter your WiFi credentials into `WIFI_SSID` and `WIFI_PASSWORD` in [WiFiConfiguration.h](firmware/config/WiFiConfiguration.h)

### Set your location

Set your location to track flights by updating the following values in [UserConfiguration.h](firmware/config/UserConfiguration.h):

- `CENTER_LAT`: Latitude of the center point to track (e.g., your home or city)
- `CENTER_LON`: Longitude of the center point
- `RADIUS_KM`: Search radius in kilometers for flights to include

### Build and flash with PlatformIO

The firmware can be built and uploaded to the ESP32 using [PlatformIO](https://platformio.org/)

---

|Item                           |Quantity|Individual Price|Bulk Price|Link                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|-------------------------------|--------|----------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|RGB Matrix **10 of these together act as the screen**                     |10      |7.21 per item   |56.85     |https://www.aliexpress.us/item/2255800358269772.html?spm=a2g0o.cart.0.0.b67938daC7qvao&mp=1&pdp_npi=6%40dis%21USD%21USD%20105.28%21USD%2056.85%21%21USD%2056.85%21%21%21%402103119c17717861824295998ef91b%2112000032067904146%21ct%21US%216564620185%21%212%210%21&_gl=1*10aplru*_gcl_au*MTA1MDMwNjU3NC4xNzcxMTcxMzM1*_ga*NDA5NjEzNjUxLjE3NzE2OTA2NzI.*_ga_VED1YSGNC7*czE3NzE3ODM0MjckbzIkZzEkdDE3NzE3ODY0NjgkajQ2JGwwJGgw&gatewayAdapt=glo2usa                                                                     |
|PSU                            |1       |16.99           |          |https://www.amazon.com/Universal-Regulated-Switching-Converter-Transformer/dp/B07PQT2Q7L/ref=sr_1_3?dib=eyJ2IjoiMSJ9.cEWptQECZPYG2UmZUYZKu27Der-60rKYmksJWPu2jfq-t_tjcURGmZPc6fqnC6qrFeLueRV8Q3iA0Yjme2BFhRX4uvcC89qr99GIQHK5FTtRDXZG35GoItHKqDTEt0kjfjwK8eRtw73qpNlFHG7D_wyzkllD-MdW4Dd7stjVi6wmBEZPdsW0PgQJNxiSliQ52wrsFaeYZM8a2uLaKulkyxIBMX6a8hWAsDA1ZcGQTts.sJkwYSu1jO9A_BELkSVmWfWshD8Z8wdUHfM-MuCyBxQ&dib_tag=se&keywords=5v%2B20a&qid=1771786531&sr=8-3&th=1                                                |
|3.3V - 5V voltage level shifter|1       |                |1.84      |https://www.aliexpress.us/item/3256806068872126.html?spm=a2g0o.detail.0.0.2210OMg5OMg5xa&mp=1&pdp_npi=6%40dis%21USD%21USD%201.84%21USD%201.84%21%21USD%201.84%21%21%21%402101e2b617717865813487690edf78%2112000036486126671%21ct%21US%216564620185%21%211%210%21&_gl=1*yn9aq9*_gcl_au*MTA1MDMwNjU3NC4xNzcxMTcxMzM1*_ga*NDA5NjEzNjUxLjE3NzE2OTA2NzI.*_ga_VED1YSGNC7*czE3NzE3ODM0MjckbzIkZzEkdDE3NzE3ODY1ODAkajYwJGwwJGgw&gatewayAdapt=glo2usa                                                                        |
|                               |        |                |          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|Items I already have           |        |                |          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|ESP-32                         |1       |9.99            |          |https://www.amazon.com/HiLetgo-ESP-WROOM-32-Development-Microcontroller-Integrated/dp/B0718T232Z/ref=sr_1_7?crid=QOLNQ7EQ7KFI&dib=eyJ2IjoiMSJ9.0mMutUw27FQh3oBplnQp1W-j79c1kFkqAhjtYy2WbRB2C73bCbQDPKPg6vtjYQ2cOyit-rw8Tk2oXiCEARMj8YkTzThMgD08OA8U0HiTIIDrUj0izC1sAf9nSEQ4hUUd0BiFGUJ6QAdGMjNa4B49RDU4hpBqhKw67Sz0LG8xFDa-NGdkMcTiNQAvY1tpgW-7mKXzXPP4ozJD4w6nTOzXvzy49iGQangh7_T-w2X1Vj0.TtOqHgXUQPfbHSQAi0XrPPqTQfGhT72rmnk0HYLESVU&dib_tag=se&keywords=esp32&qid=1771787487&sprefix=esp3%2Caps%2C231&sr=8-7&th=1|
|Filament                       |        |                |          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
