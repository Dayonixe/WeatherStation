# Guide manual

Team : Théo Pirouelle

<a href="https://www.arduino.cc/">
  <img src="https://img.shields.io/badge/language-Arduino-008184?style=flat-square" alt="laguage-arduino" />
</a>

---

## Table of contents
- [Materials](#materials)
- [Requirements](#requirements)
  * [OpenWeatherMap](#openweathermap)
  * [ThingSpeak](#thingspeak)
- [Installation guides](#installation-guides)
  * [Install USB-to-Serial](#install-usb-to-serial)
  * [Install Arduino IDE for ESP8266](#install-arduino-ide-for-esp8266)
  * [Burning Firmware to ESP8266](#burning-firmware-to-esp8266)
  * [Adding Library](#adding-library)
  * [Code customisation](#code-customisation)
- [Connecting components](#connecting-components)
- [Results](#results)
- [Errors](#errors)

---

# Materials

- [ESP8266-12E](https://fr.aliexpress.com/item/1005004513260449.html?spm=a2g0o.store_pc_home.0.0.66901f368eiCwl&pdp_npi=3%40dis%21EUR%21%E2%82%AC%202%2C13%21%E2%82%AC%202%2C13%21%21%21%21%21%40%2112000029439779507%21sh%21%21&gatewayAdapt=glo2fra)
- Sensors:
  - Pressure ([BMP180](https://www.az-delivery.de/fr/products/azdelivery-gy-68-bmp180-barometrischer-sensor-luftdruck-modul-fur-arduino-und-raspberry-pi))
  - Temperature & Humidity ([DHT11](https://www.az-delivery.de/fr/products/dht-11-temperatursensor-modul))
  - Light ([BH1750FVI](https://www.amazon.fr/Gy-30-Sourcingmap-Bh1750fvi-Digital-intensit%C3%A9-Arduino/dp/B076HL9QW7/ref=sr_1_12?keywords=bh1750fvi&qid=1694098999&sr=8-12))
- [OLED Display](https://www.az-delivery.de/fr/products/0-96zolldisplay)
- 15 Wires

---

# Requirements

## OpenWeatherMap

1. Sign up new account at https://home.openweathermap.org/users/sign_in
2. Get the API keys at https://home.openweathermap.org/api_keys

<p align="center">
  <img src="/doc/openweathermap.png" alt="OpenWeatherMap"/>
</p>

## ThingSpeak

1. Sign up new account at https://www.mathworks.com/mwaccount/register
2. Create a new channel and configure it:

<p align="center">
  <img src="/doc/thingspeak1.png" alt="ThingSpeak"/>
</p>

3. Set the channel to public:

<p align="center">
  <img src="/doc/thingspeak2.png" alt="ThingSpeak"/>
</p>

4. Get the API keys of the channel:

<p align="center">
  <img src="/doc/thingspeak3.png" alt="ThingSpeak"/>
</p>

---

# Installation guides

## Install USB-to-Serial

If, when you connect your ESP8266 card to your computer via USB, you do not see it in the Device Manager, you need to install the [USB-to-Serial](https://github.com/Dayonixe/WeatherStation/tree/main/tools) driver.

<p align="center">
  <img src="/doc/devicemanager.png" alt="Device Manager"/>
</p>

## Install Arduino IDE for ESP8266

> **Warning**<br>
> For this project, I used version `1.8.4` of the [Arduino IDE](https://www.arduino.cc/en/software/OldSoftwareReleases), other versions may not work with my source code.

1. Open Arduino IDE
2. *File > Preferences*
3. Insert the following link in the "Additional Boards Manager URLs" text box: http://arduino.esp8266.com/stable/package_esp8266com_index.json

<p align="center">
  <img src="/doc/arduinopreferences.png" alt="Arduino Preferences"/>
</p>

4. Click on "OK" to close the dialog box.
5. Go to *Tools > Board > Board Manager* and click on this option.
6. Type "ESP8266" in the text box, and install the "ESP8266 by ESP8266 Community" option.

<p align="center">
  <img src="/doc/arduinoboardmanager.png" alt="Arduino Board Manager"/>
</p>

7. Once the installation process is complete (it may take 1 minute or more), you can close the dialog box by clicking on the "Close" button.
8. Go back to *Tools > Board* and you should see some new board choices appear at the bottom of the list.
9. Select `NodeMCU 1.0 (ESP-12E Module)`.
10. Go to *Tools > Port* and select the correct port (as seen in the Device Manager, in my case it's `COM3`).


## Burning Firmware to ESP8266

1. The ESP8266 card must be properly connected to the computer via the data cable.
2. Use [`ESP8266Flasher.exe`](https://github.com/Dayonixe/WeatherStation/tree/main/tools/flasher) burning `Ai-Thinker_ESP8266_DOUT_8Mbit_v1.5.4.1-a_20171130.bin` for the ESP8266.
3. Operation as shown (as before, make sure you select the correct port and click on the "Flash" button):

<p align="center">
  <img src="/doc/flasher1.png" alt="Flasher"/>
</p>

<p align="center">
  <img src="/doc/flasher2.png" alt="Flasher"/>
</p>


## Adding Library

1. In *Sketch > Include Library > Add .ZIP Library...*, import the [`esp8266-weather-station-master.zip`](https://github.com/Dayonixe/WeatherStation/tree/main/tools/library) library.
2. In *Sketch > Include Library > Add .ZIP Library...*, import the [`json-streaming-parser-master.zip`](https://github.com/Dayonixe/WeatherStation/tree/main/tools/library) library.
3. In *Sketch > Include Library > Add .ZIP Library...*, import the [`esp8266-oled-ssd1306-master.zip`](https://github.com/Dayonixe/WeatherStation/tree/main/tools/library) library.
4. In *Sketch > Include Library > Manage Libraries...*, type "Adafruit_BMP085" in the text box, and install the "Adafruit BMP085 Library by Adafruit" option:

<p align="center">
  <img src="/doc/arduinolibrarymanager.png" alt="Arduino Library Manager"/>
</p>


## Code customisation

1. Open the main code.
2. Update the `WIFI_SSID` and the `WIFI_PWD`.
3. Update the OpenWeatherMap API key `OPEN_WEATHER_MAP_APP_ID`.
4. Update the ThingSpeak API key `api_key`.

---

# Connecting components

<p align="center">
  <img src="/doc/connectingcomponents.png" alt="Connecting Components"/>
</p>

It is preferable to carry out the wiring with the power off.

---

# Results

<p align="center">
  <img src="/doc/thingspeakchannel.png" alt="ThingSpeak Channel"/>
</p>

<p align="center">
  <img src="/doc/arduinoserialmonitor.png" alt="Arduino Serial Monitor"/>
</p>

<p align="center">
  <img src="/doc/screen.png" alt="Screen"/>
</p>

---

# Errors

If the following error occurs in the Arduino IDE:
```
C:\Users\Admin\Documents\Arduino\libraries\esp8266-weather-station-master\src\TimeClient.cpp: In member function 'long int TimeClient::getCurrentEpochWithUtcOffset()':
C:\Users\Admin\Documents\Arduino\libraries\esp8266-weather-station-master\src\TimeClient.cpp:124:67:
error: invalid operands of types 'double' and 'long int' to binary 'operator%'
  return round(getCurrentEpoch() + 3600 * myUtcOffset + 86400L) % 86400L;
Using library Adafruit_BMP085_Library at version 1.0.0 in folder:
C:\Users\Admin\Documents\Arduino\libraries\Adafruit_BMP085_Library
exit status 1
Error compiling for board NodeMCU 1.0 (ESP-12E Module).
```

- Recommended configuration for Arduino IDE version 1.8.4 for Windows
- In *Sketch > Include Library > Manage Libraries...*, as "Type" select `Installed`, type "weather" in the text box, update "ESP8266 Weather Station by ThingPulse" to at least version `1.6.5`, and click the "Update" button.
