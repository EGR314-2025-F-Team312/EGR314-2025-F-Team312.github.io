---
title: ESP32 C++ Code Aappendix
---

## Control Panel Code (C++)

```
#include <Arduino.h>
#include <esp_now.h>
#include <esp_wifi.h>
#include <WiFi.h>
#include <string.h>
#include <math.h>

//LED Pins
const int temp1Pin     = 4;
const int humidity1Pin = 5;
const int pressure1Pin = 6;
const int wildfire1Pin = 7;

const int temp2Pin     = 9;
const int humidity2Pin = 10;
const int pressure2Pin = 11;
const int wildfire2Pin = 12;

//PWM settings
const int freq = 5000;
const int resolution = 8;   // 0-255

//Fade state
int duty1 = 0, dir1 = +1;
int duty2 = 0, dir2 = +1;
int duty3 = 0, dir3 = +1;
int duty4 = 0, dir4 = +1;

const uint32_t fadeIntervalMs = 15;
const int fadeSize = 5;

uint32_t lastFadeStep1 = 0;
uint32_t lastFadeStep2 = 0;
uint32_t lastFadeStep3 = 0;
uint32_t lastFadeStep4 = 0;

// data payload
typedef struct __attribute__((packed)) {
  float    tempC;         // °C
  float    pressure_hPa;  // hPa
  float    humidity_pct;  // %RH
  uint32_t timestamp_ms;  // sender millis()
} telemetry_struct;

telemetry_struct receivedData;

// Latest readings accessible from loop()
volatile float latestTempC = NAN;
volatile float latestPressure_hPa = NAN;
volatile float latestHumidity_pct = NAN;
volatile uint32_t latestTimestamp = 0;

bool wildfireActive = false; 

static void printMACAddress(const uint8_t *mac) {
  Serial.printf("%02X:%02X:%02X:%02X:%02X:%02X\n",
                mac[0], mac[1], mac[2], mac[3], mac[4], mac[5]);
}

static void printStaMac() {
  uint8_t mac[6];
  esp_wifi_get_mac(WIFI_IF_STA, mac);
  Serial.printf("%02X:%02X:%02X:%02X:%02X:%02X\n",
                mac[0], mac[1], mac[2], mac[3], mac[4], mac[5]);
}

// ESP-NOW receive callback
void OnDataRecv(const esp_now_recv_info_t *info, const uint8_t *incomingData, int len) {
  if (len != (int)sizeof(telemetry_struct)) {
    Serial.printf("Received %d bytes (expected %d). Ignoring.\n",
                  len, (int)sizeof(telemetry_struct));
    return;
  }

  memcpy(&receivedData, incomingData, sizeof(receivedData));

  // Update "latest" globals
  latestTempC = receivedData.tempC;
  latestPressure_hPa = receivedData.pressure_hPa;
  latestHumidity_pct = receivedData.humidity_pct;
  latestTimestamp = receivedData.timestamp_ms;

  Serial.print("From: ");
  printMACAddress(info->src_addr);

  Serial.printf("Temp: %.2f C, Pressure: %.2f hPa, Humidity: %.2f %% | timestamp_ms: %lu\n\n",
                receivedData.tempC,
                receivedData.pressure_hPa,
                receivedData.humidity_pct,
                (unsigned long)receivedData.timestamp_ms);
}

static void stepFade(int pin, int &duty, int &dir) {
  duty += dir * fadeSize;
  if (duty >= 255) { duty = 255; dir = -1; }
  if (duty <= 0)   { duty = 0;   dir = +1; }
  ledcWrite(pin, duty); 
}

void setup() {
  Serial.begin(115200);

  // PWM attach
  ledcAttach(temp1Pin,     freq, resolution);
  ledcAttach(humidity1Pin, freq, resolution);
  ledcAttach(pressure1Pin, freq, resolution);
  ledcAttach(wildfire1Pin, freq, resolution);

  ledcAttach(temp2Pin,     freq, resolution);
  ledcAttach(humidity2Pin, freq, resolution);
  ledcAttach(pressure2Pin, freq, resolution);
  ledcAttach(wildfire2Pin, freq, resolution);

  // Start them OFF
  ledcWrite(temp1Pin, 0);
  ledcWrite(humidity1Pin, 0);
  ledcWrite(pressure1Pin, 0);
  ledcWrite(wildfire1Pin, 0);

  ledcWrite(temp2Pin, 0);
  ledcWrite(humidity2Pin, 0);
  ledcWrite(pressure2Pin, 0);
  ledcWrite(wildfire2Pin, 0);

  WiFi.mode(WIFI_STA);
  delay(200);

  Serial.print("Receiver MAC: ");
  printStaMac();

  esp_wifi_set_channel(1, WIFI_SECOND_CHAN_NONE);

  if (esp_now_init() != ESP_OK) {
    Serial.println("Error initializing ESP-NOW");
    while (true) delay(100);
  }

  if (esp_now_register_recv_cb(OnDataRecv) != ESP_OK) {
    Serial.println("Error registering ESP-NOW receive callback");
    while (true) delay(100);
  }

  Serial.println("Receiver ready.");
}

void loop() {
  uint32_t now = millis();

  // Copy volatile globals into locals
  float tempC = latestTempC;
  float hum   = latestHumidity_pct;
  float pres  = latestPressure_hPa;

  // - If temp >= 40C -> fade temp1 LED
  if (!isnan(tempC) && tempC >= 30.0f) {
    if (now - lastFadeStep1 >= fadeIntervalMs) {
      lastFadeStep1 = now;
      stepFade(temp1Pin, duty1, dir1);
    }
  } else {
    ledcWrite(temp1Pin, 0); // off when not alarming
  }

  // - If humidity <= 20% -> fade humidity1 LED
  if (!isnan(hum) && hum <= 20.0f) {
    if (now - lastFadeStep2 >= fadeIntervalMs) {
      lastFadeStep2 = now;
      stepFade(humidity1Pin, duty2, dir2);
    }
  } else {
    ledcWrite(humidity1Pin, 0);
  }

  // - If pressure <= some threshold -> fade pressure1 LED
  if (!isnan(pres) && pres >= 960.0f) {
    if (now - lastFadeStep3 >= fadeIntervalMs) {
      lastFadeStep3 = now;
      stepFade(pressure1Pin, duty3, dir3);
    }
  } else {
    ledcWrite(pressure1Pin, 0);
  }

  bool wildfireAlarm =
    (!isnan(tempC) && tempC >= 30.0f && !isnan(hum)  && hum  <= 20.0f) ||
    (!isnan(tempC) && tempC >= 30.0f && !isnan(pres) && pres >= 960.0f) ||
    (!isnan(hum)   && hum  <= 20.0f && !isnan(pres) && pres >= 960.0f);

  if (wildfireAlarm) {
    if (now - lastFadeStep4 >= fadeIntervalMs) {
      lastFadeStep4 = now;
      stepFade(wildfire1Pin, duty4, dir4);
    }
  } else {
    ledcWrite(wildfire1Pin, 0);
  }


  //to keep fade staying smooth
  delay(1);
}
```

## Weather Station Code (C++)

```
#include <Arduino.h>
#include <Wire.h>
#include <WiFi.h>
#include <esp_wifi.h>
#include <esp_now.h>

#include <Adafruit_Sensor.h>
#include <Adafruit_BME280.h>

// ESP-NOW receiver MAC Address (control panel)
uint8_t receiverAddress[] = {0x48, 0xCA, 0x43, 0x4E, 0x59, 0x90}; // receiver MAC

// I2C pins
static constexpr int I2C_SDA = 8;
static constexpr int I2C_SCL = 9;

// BME280 object
Adafruit_BME280 bme;              // I2C
static constexpr uint8_t BME_ADDR = 0x76;  // SDO grounded -> 0x76

// data payload
typedef struct __attribute__((packed)) {
  float tempC;          // degrees C
  float pressure_hPa;   // hPa
  float humidity_pct;   // %RH
  uint32_t timestamp_ms;
} telemetry_struct;

telemetry_struct myData;

//callback for ESP-NOW
void onDataSent(const wifi_tx_info_t *tx_info, esp_now_send_status_t status) {
  Serial.print("ESP-NOW send status: ");
  Serial.println(status == ESP_NOW_SEND_SUCCESS ? "SUCCESS" : "FAIL");
}

void setup() {
  Serial.begin(115200);
  delay(200);

  //I2C initializing
  Wire.begin(I2C_SDA, I2C_SCL);
  Wire.setClock(100000);  // safe for BME280

  //BME280 initializing
  bool ok = bme.begin(BME_ADDR);
  if (!ok) {
    //check other board address
    ok = bme.begin(0x77);
  }
  if (!ok) {
    Serial.println("BME280 not found at 0x76 or 0x77. Check wiring/power!");
    while (true) delay(100);
  }
  Serial.println("BME280 found.");

  //ESP-NOW initialize
  WiFi.mode(WIFI_STA);

  //set wifi channel to 1
  esp_wifi_set_channel(1, WIFI_SECOND_CHAN_NONE);

  if (esp_now_init() != ESP_OK) {
    Serial.println("Error initializing ESP-NOW");
    while (true) delay(100);
  }

  esp_now_register_send_cb(onDataSent);

  esp_now_peer_info_t peerInfo = {};
  memcpy(peerInfo.peer_addr, receiverAddress, sizeof(receiverAddress));
  peerInfo.channel = 1;
  peerInfo.ifidx = WIFI_IF_STA;
  peerInfo.encrypt = false;

  if (esp_now_add_peer(&peerInfo) != ESP_OK) {
    Serial.println("Failed to add peer");
    while (true) delay(100);
  }

  Serial.println("Sender ready.");
}

void loop() {
  // Read BME280
  float tempC = bme.readTemperature();             // °C
  float pressure_hPa = bme.readPressure() / 100.0; // Pa -> hPa
  float humidity = bme.readHumidity();             // %

  // Basic sanity check for sensor wiring
  if (isnan(tempC) || isnan(pressure_hPa) || isnan(humidity)) {
    Serial.println("BME280 read returned NaN (check sensor/wiring).");
    delay(1000);
    return;
  }

  myData.tempC = tempC;
  myData.pressure_hPa = pressure_hPa;
  myData.humidity_pct = humidity;
  myData.timestamp_ms = millis();

  Serial.printf("T=%.2f C, P=%.2f hPa, H=%.2f %% -> sending...\n",
                tempC, pressure_hPa, humidity);

  esp_err_t result = esp_now_send(receiverAddress, (uint8_t*)&myData, sizeof(myData));
  if (result == ESP_OK) Serial.println("Sent OK");
  else Serial.println("ESP-NOW send error");

  delay(2000);
}
```