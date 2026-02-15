# 💧 IoT-Based Smart Drip Irrigation Leakage & Pressure Monitoring System

<p align="center">
  <img src="https://img.shields.io/badge/ESP32-E7352C?style=for-the-badge&logo=espressif&logoColor=white" alt="ESP32"/>
  <img src="https://img.shields.io/badge/IoT-00979D?style=for-the-badge&logo=arduino&logoColor=white" alt="IoT"/>
  <img src="https://img.shields.io/badge/Agriculture-10B981?style=for-the-badge&logo=leaflet&logoColor=white" alt="Agriculture"/>
  <img src="https://img.shields.io/badge/Smart_Farming-34D399?style=for-the-badge" alt="Smart Farming"/>
</p>

## 📖 Overview

An intelligent IoT-based irrigation system that monitors water pressure, detects leakages, controls drip irrigation valves, and provides real-time alerts. Designed to optimize water usage in agriculture, reduce waste, and prevent crop damage due to irrigation failures.

## ✨ Key Features

- 💧 **Smart Water Management** - Automated drip irrigation control
- 📊 **Pressure Monitoring** - Real-time water pressure tracking
- 🚰 **Leak Detection** - Automatic detection of pipe leaks and bursts
- 🌡️ **Soil Moisture Sensing** - Monitor soil moisture levels
- 📱 **Remote Control** - Control valves from anywhere via mobile/web
- 🔔 **Instant Alerts** - SMS/Email notifications for leaks and low pressure
- 📈 **Water Usage Analytics** - Track daily/weekly/monthly consumption
- ⏰ **Scheduled Irrigation** - Set automatic watering schedules
- 🌐 **Cloud Logging** - Store historical data for analysis
- 💡 **Energy Efficient** - Solar-powered option available

## 🛠️ Hardware Components

| Component | Quantity | Purpose |
|-----------|----------|---------|
| ESP32 Development Board | 1 | Main controller |
| Water Pressure Sensor (0-1.2 MPa) | 1 | Pressure monitoring |
| Water Flow Sensor (YF-S201) | 1 | Flow rate measurement |
| Soil Moisture Sensor (Capacitive) | 3 | Soil moisture detection |
| Solenoid Valve (12V) | 3 | Water flow control |
| Relay Module (4-Channel) | 1 | Valve control |
| DHT22 Sensor | 1 | Temperature & humidity |
| 16x2 LCD Display (I2C) | 1 | Local status display |
| Buzzer | 1 | Audio alerts |
| 12V 5A Power Supply | 1 | System power |
| ADS1115 ADC (16-bit) | 1 | Analog sensor reading |
| Waterproof Enclosure | 1 | Outdoor protection |

## 📐 System Architecture

```
                    ┌─────────────────┐
                    │  Cloud Platform │
                    │  (ThingSpeak/   │
                    │   Blynk/MQTT)   │
                    └────────┬────────┘
                             │
                          WiFi│
                             │
                    ┌────────▼────────┐
                    │     ESP32       │
                    │   Controller    │
                    └─┬───┬───┬───┬───┘
                      │   │   │   │
        ┌─────────────┼───┼───┼───┼─────────────┐
        │             │   │   │   │             │
    ┌───▼───┐    ┌───▼──┐│   │   │   ┌────▼────┐
    │Pressure│   │Flow  ││   │   │   │Solenoid │
    │Sensor  │   │Sensor││   │   │   │Valves   │
    └────────┘   └──────┘│   │   │   └─────────┘
                      ┌───▼───▼───▼──┐
                      │Soil Moisture │
                      │   Sensors    │
                      └──────────────┘
```

## 💻 Software Requirements

- **Arduino IDE** 2.x or **PlatformIO**
- **ESP32 Board Package**
- **Required Libraries:**
  - `WiFi.h` - WiFi connectivity
  - `PubSubClient.h` or `BlynkSimpleEsp32.h` - IoT platform
  - `Wire.h` - I2C communication
  - `LiquidCrystal_I2C.h` - LCD display
  - `DHT.h` - Temperature/humidity sensor
  - `Adafruit_ADS1X15.h` - ADC module
  - `ArduinoJson.h` - JSON data handling
  - `NTPClient.h` - Time synchronization

## 📦 Installation

### 1. Hardware Setup

#### Pin Connections

| ESP32 Pin | Component | Connection |
|-----------|-----------|------------|
| GPIO34 | Pressure Sensor | Analog output |
| GPIO35 | Flow Sensor | Pulse output |
| GPIO32 | DHT22 | Data pin |
| GPIO21 | ADS1115 | I2C SDA |
| GPIO22 | ADS1115 | I2C SCL |
| GPIO25 | Relay 1 | Valve 1 control |
| GPIO26 | Relay 2 | Valve 2 control |
| GPIO27 | Relay 3 | Valve 3 control |
| GPIO33 | Buzzer | Audio alert |
| GPIO21 | LCD | I2C SDA |
| GPIO22 | LCD | I2C SCL |
| 3.3V | Sensors | Power |
| GND | All | Ground |

### 2. Software Installation

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/smart-drip-irrigation.git
cd smart-drip-irrigation

# Open in Arduino IDE
# Install ESP32 board support
# Install required libraries
```

### 3. Configuration

Edit `config.h`:

```cpp
// WiFi Credentials
#define WIFI_SSID "Your_WiFi_Name"
#define WIFI_PASSWORD "Your_Password"

// ThingSpeak/Blynk Settings
#define THINGSPEAK_API_KEY "YOUR_API_KEY"
#define BLYNK_AUTH "YOUR_BLYNK_TOKEN"

// Irrigation Zones
#define NUM_ZONES 3
#define ZONE1_NAME "Garden Area"
#define ZONE2_NAME "Vegetable Patch"
#define ZONE3_NAME "Lawn Area"

// Alert Settings
#define PRESSURE_LOW_THRESHOLD 0.2  // MPa
#define PRESSURE_HIGH_THRESHOLD 1.0 // MPa
#define LEAK_FLOW_THRESHOLD 5.0     // L/min
#define SOIL_DRY_THRESHOLD 30       // %
#define SOIL_WET_THRESHOLD 70       // %

// Notification
#define ENABLE_SMS true
#define PHONE_NUMBER "+919876543210"
#define ENABLE_EMAIL true
#define EMAIL_ADDRESS "your@email.com"
```

### 4. Upload Code

1. Connect ESP32 via USB
2. Select Board: **ESP32 Dev Module**
3. Select Port: Your COM port
4. Click **Upload**

## 🚀 Usage

### Initial Setup

1. **Power On System**
   - ESP32 boots and connects to WiFi
   - LCD shows "System Ready"
   - All sensors initialize

2. **Configure Zones**
   - Access web dashboard
   - Set irrigation schedule for each zone
   - Define soil moisture thresholds

3. **Test System**
   - Manually trigger each valve
   - Verify sensors are reading correctly
   - Check alert notifications

### Automatic Operation

The system runs autonomously based on:
- **Scheduled Times** - Water at preset times
- **Soil Moisture** - Water when soil is dry
- **Weather Data** - Skip if rain detected

### Manual Control

**Via Web Dashboard:**
- Open `http://ESP32_IP_ADDRESS`
- Click valve buttons to control
- View live sensor data

**Via Blynk App:**
- Download Blynk app
- Scan QR code (in docs folder)
- Control from anywhere

### Monitoring

**LCD Display Shows:**
```
Zone1: ON  P:0.8MPa
F:12L/m  SM:45%
```

**Dashboard Displays:**
- Real-time pressure graph
- Flow rate meter
- Soil moisture levels
- Water usage statistics
- Alert history

## 🔍 Leak Detection Algorithm

```cpp
void detectLeak() {
  // Calculate expected flow based on open valves
  float expectedFlow = calculateExpectedFlow();
  float actualFlow = readFlowSensor();
  float flowDifference = abs(actualFlow - expectedFlow);
  
  // If actual flow is much higher than expected
  if(flowDifference > LEAK_FLOW_THRESHOLD) {
    leakDetected = true;
    
    // Close all valves
    closeAllValves();
    
    // Send alert
    sendAlert("LEAK DETECTED! System shutdown.");
    
    // Sound buzzer
    activateBuzzer();
    
    // Log incident
    logToCloud("Leak detected at " + getCurrentTime());
  }
}
```

### Leak Detection Indicators

| Scenario | Pressure | Flow | Action |
|----------|----------|------|--------|
| Normal | 0.4-0.8 MPa | As expected | Continue |
| Small leak | Gradual drop | Slightly high | Warning alert |
| Major leak | Rapid drop | Very high | Emergency shutdown |
| Pipe burst | Drops to 0 | Maximum | Emergency + SMS |
| Blockage | Rises high | Low/zero | Valve control |

## 📊 Data Visualization

### ThingSpeak Integration

```cpp
void updateThingSpeak() {
  ThingSpeak.setField(1, pressure);
  ThingSpeak.setField(2, flowRate);
  ThingSpeak.setField(3, soilMoisture1);
  ThingSpeak.setField(4, soilMoisture2);
  ThingSpeak.setField(5, soilMoisture3);
  ThingSpeak.setField(6, temperature);
  ThingSpeak.setField(7, humidity);
  ThingSpeak.setField(8, waterUsageToday);
  
  ThingSpeak.writeFields(channelID, apiKey);
}
```

Access your ThingSpeak dashboard to view:
- Real-time graphs
- Historical trends
- Water consumption analysis
- Export data to CSV

## 🔔 Alert System

### Alert Types

1. **Critical Alerts** (Immediate SMS + Email + Buzzer)
   - Major leak detected
   - Pipe burst
   - System malfunction

2. **Warning Alerts** (Email + Dashboard)
   - Low water pressure
   - High water pressure
   - Small leak detected
   - Soil too dry

3. **Info Alerts** (Dashboard only)
   - Irrigation started
   - Irrigation completed
   - Daily water usage summary

### Notification Channels

- 📱 **SMS** - Using Twilio API
- 📧 **Email** - Using SMTP
- 📲 **Push Notification** - Via Blynk
- 🔊 **Buzzer** - Local audio alert
- 💡 **LED** - Visual status indicator

## 🌱 Irrigation Scheduling

### Schedule Format

```json
{
  "zone1": {
    "enabled": true,
    "schedule": [
      {"time": "06:00", "duration": 30},
      {"time": "18:00", "duration": 20}
    ],
    "soil_trigger": 35,
    "rain_skip": true
  }
}
```

### Smart Scheduling Features

- **Weather Integration** - Skip if rain is forecast
- **Adaptive Timing** - Adjust based on season
- **Soil-Based** - Water only when needed
- **Vacation Mode** - Minimal watering

## 🔧 Calibration

### Pressure Sensor Calibration

```cpp
void calibratePressureSensor() {
  // Known pressure (use manual gauge)
  float knownPressure = 0.5; // MPa
  
  // Read sensor
  int rawValue = analogRead(PRESSURE_PIN);
  float voltage = rawValue * (3.3 / 4095.0);
  
  // Calculate calibration factor
  PRESSURE_CALIBRATION = knownPressure / voltage;
}
```

### Flow Sensor Calibration

```cpp
void calibrateFlowSensor() {
  // Collect known volume
  float knownVolume = 10.0; // Liters
  
  // Count pulses
  unsigned long pulseCount = countPulses(60); // 60 seconds
  
  // Calculate calibration factor
  FLOW_CALIBRATION = knownVolume / pulseCount;
}
```

## 🐛 Troubleshooting

| Issue | Possible Cause | Solution |
|-------|----------------|----------|
| Valves not opening | Relay not working | Check relay connections and power |
| Wrong pressure reading | Sensor not calibrated | Run calibration routine |
| No leak detection | Threshold too high | Lower LEAK_FLOW_THRESHOLD |
| WiFi disconnecting | Weak signal | Use WiFi extender or repositioning |
| False leak alerts | Flow sensor dirty | Clean sensor, recalibrate |
| LCD blank | I2C address wrong | Scan for I2C devices, update address |

## 📈 Water Savings

This system can save up to **40-60% water** compared to traditional irrigation:

- ✅ Water only when soil needs it
- ✅ Detect and stop leaks immediately
- ✅ Optimal pressure prevents waste
- ✅ Scheduled watering at best times
- ✅ Weather-aware irrigation

## 🌟 Future Enhancements

- [ ] Weather forecast integration (OpenWeatherMap API)
- [ ] Predictive maintenance using ML
- [ ] Multi-crop specific irrigation
- [ ] Fertilizer injection control
- [ ] Mobile app (Flutter/React Native)
- [ ] Solar panel integration
- [ ] LoRa support for remote farms
- [ ] Integration with farm management systems

## 🎥 Demo

### Video Demonstration
[Add YouTube link]

### Installation Guide
[Add video tutorial link]

## 🤝 Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create feature branch
3. Commit your changes
4. Submit pull request

## 📄 License

MIT License - see [LICENSE](LICENSE)

## 👤 Author

**Ajay Kumar Pujari**
- Email: ajaykumarpujari22@gmail.com
- GitHub: [@YOUR_USERNAME](https://github.com/YOUR_USERNAME)
- LinkedIn: [Your Profile](https://linkedin.com/in/YOUR_PROFILE)

## 🙏 Acknowledgments

- Agricultural research community
- Open-source IoT platforms
- ESP32 developers community

## 📚 Resources

- [ESP32 Datasheet](https://www.espressif.com/en/products/socs/esp32)
- [Drip Irrigation Guide](https://www.fao.org/land-water/water/drip-irrigation)
- [ThingSpeak Documentation](https://thingspeak.com/docs)

---

⭐ If this project helped you, please star it!

**Tags:** `iot` `agriculture` `smart-farming` `irrigation` `esp32` `water-management` `leak-detection` `embedded-systems` `automation` `sensors`
