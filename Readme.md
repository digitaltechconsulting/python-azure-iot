**Python Script To Read weather Data**

In this sample, I will how you how to build [simple circuit](https://github.com/BuildAzure/BuildAzure.IoT.Adafruit.BME280) to collect weather data from [BME 280 sensor](https://core-electronics.com.au/adafruit-bme280-i2c-or-spi-temperature-humidity-pressure-sensor.html?utm_source=google_shopping&gclid=Cj0KCQjwvb75BRD1ARIsAP6LcqtezeB4Wn_Dn_3IYdkcl1I6dAAZWYlhJrbtzBnTKmmClYgyOd5UCuUaAhSJEALw_wcB).  We will use [Adafruit BME280 Library](https://circuitpython.readthedocs.io/projects/bme280/en/latest/) to collect this data.  Subsequently, we will feed this data to Azure IoT hub using [azure-iot-sdk-python](https://github.com/Azure/azure-iot-sdk-python/tree/master/azure-iot-device)

**Circuit diagram**

<img src="https://github.com/BuildAzure/BuildAzure.IoT.Adafruit.BME280/blob/master/BME280Fritzing.png?raw=true">


Source : https://github.com/BuildAzure/BuildAzure.IoT.Adafruit.BME280


**Read data from Sensor**

Now lets implement python script to read temperature, humidity , pressure and altitude values from BME 280 sensor.

 - We will use FileZilla to move files across raspberry pi device.
    - Launch FileZilla
    - Click on Site Manager
    - New Site
    - 'pi-weather-station'
    - Select Protocol `SFTP`
    - Input host details
    - Provide username and password ( pi / password )
 - SSH to raspberry pi
 - Navigate to [Adafruit BME280 Library](https://circuitpython.readthedocs.io/projects/bme280/en/latest/) to copy sample code.


**Install python package**

`sudo pip3 install adafruit-circuitpython-bme280`

Python script 

````python
import board
import digitalio
import busio
import time
import adafruit_bme280

# Create library object using our Bus I2C port
i2c = busio.I2C(board.SCL, board.SDA)
bme280 = adafruit_bme280.Adafruit_BME280_I2C(i2c)

# change this to match the location's pressure (hPa) at sea level
bme280.sea_level_pressure = 1013.25

while True:
    print("\nTemperature: %0.1f C" % bme280.temperature)
    print("Humidity: %0.1f %%" % bme280.humidity)
    print("Pressure: %0.1f hPa" % bme280.pressure)
    print("Altitude = %0.2f meters" % bme280.altitude)
    time.sleep(2)
````
Source: https://circuitpython.readthedocs.io/projects/bme280/en/latest/



