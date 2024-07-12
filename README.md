## Design and program any electronic circuit that contains an ESP, along with any sensor or electronic piece, and explain the function of the circuit :
#### Using the wokwi application, I ran the circuit and the code:
* 1-ESP32 microcontroller.
* 2-DHT22 temperature and humidity sensor
* 3-Breadboard and jumper wires
Circuit function:
## The ESP microcontroller will be responsible for connecting to the Wi-Fi network and retrieving weather data from an online source. It will also collect data from the temperature and humidity sensor.
#### The circuit can be designed as follows:
* 1- From ESP connect 3v3 with vcc. 
* 2- From the ESP, connect GND1 to GND in the sensor. 
* 3- From ESP, connect D15 to SDA from ESP.
* 4- Add a screen size 2*16. 
* 5 - Add the vcc code and connect it to the screen. 
* 6- Add the GND code and connect it to the screen. 
* 7- From ESP, connect D21 with the screen to SDA. 
* 8- From ESP, connect D22 to the screen with SCL.
#### CODE:
```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 16
#define LCD_LINES   2

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();

}

void loop() {

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  lcd.print("Wokwi Online IoT");

  delay(1000);
}
```
![لقطة شاشة 2024-07-12 140628](https://github.com/user-attachments/assets/e3fcfdc2-01c9-4142-9f98-89ffe437793b)
