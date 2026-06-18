# Sense Pi V1 - Technical Documentation

Sense Pi is a compact and highly capable desktop smart assistant based on the **Raspberry Pi Pico 2W**, designed to operate in a Do-It-Yourself Shield configuration. With its advanced sensor array, uninterruptible power supply (UPS) feature, and internet connectivity, it functions as both an intelligent information dashboard and a portable measurement laboratory.

## 1\. Hardware and Components

The project features a modular architecture. All components used in the build are categorized below:

### Core Control and Display Unit

- **Main Controller:** Raspberry Pi Pico 2W (Dual-Core RP2350 Processor, 150MHz)
- **Display:** 2.8-inch SPI TFT LCD Touch Panel (320x240 Pixel resolution, XPT2046 Touch driver) - _Mounted directly as a shield onto the Pico._
- **Input Device:** KY-040 Rotary Encoder (For menu navigation and selection)
- **Audio Output:** Passive Piezo Buzzer (For alarms and audible feedback)

### Sensor and Lighting Array

- **DHT-11:** Digital Temperature and Humidity Sensor (Monitors room climate).
- **MPU-6050:** 6-Axis Accelerometer and Gyroscope (Utilized for the Sismometer and Digital Spirit Level applications).
- **HC-SR04:** Ultrasonic Distance Sensor (For distance measurement and obstacle detection).
- **QRE1113 (IR):** Infrared Reflectance Sensor (For contactless gesture-based screensaver activation).
- **3W Power LED Module:** High-power light source utilized in the Flashlight (Torch) application for emergency illumination.

### Power and UPS System (Uninterruptible Power Supply)

An integrated battery management system that ensures continuous operation during power cuts and enables full portability.

- **Batteries:** 3 x 18650 Lithium-Ion Batteries (Connected in series, providing a total capacity of 11.1V - 12.6V).
- **Protection Circuit (BMS):** 1 x 3S 20A BMS Board (For safe battery charge/discharge regulation).
- **Voltage Regulator:** 1 x Dual USB Output 5V 3A Step-Down Regulator (Safely reduces the 12V battery bank voltage to a stable 5V for the device).
- **Charging Module:** 1 x 3S 2A Type-C Charging Module (Enables fast charging of the battery pack via standard Type-C power adapters).

## 2\. Raspberry Pi Pico 2W Technical Specifications

The core intelligence of Sense Pi is driven by the Pico 2W, delivering exceptional performance for smooth UI rendering:

- **Processor:** RP2350 (Arm Cortex-M33 running at 150 MHz), providing hardware-accelerated fluid interface transitions.
- **Wireless Connectivity:** Wi-Fi 4 (802.11n) support to automatically fetch weather data, internet synchronized time, exchange rates, and calendar events over the network.
- **Memory:** 520 KB internal SRAM, offering sufficient overhead to handle colorful graphics and real-time sensor processing (such as active earthquake waveforms).
- **Storage:** 4 MB Flash memory, hosting the complete software stack, custom fonts, and graphical user interface icons.

## 3\. Connection Guide (Pinout)

Since the display module is plugged into the back of the Pico as a custom shield, the SPI lines remain fixed. External modules and peripheral devices must be wired according to the hardware pin configuration map below:

| **Module Name**                                   | **Module Pin**                                            | **Pico Target Pin**                             | **Physical Pin No**                                         | **Voltage / Notes**                                                                                                |
| ------------------------------------------------- | --------------------------------------------------------- | ----------------------------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Rotary Encoder**<br><br>_(Menu Control)_        | CLK<br><br>DT<br><br>SW<br><br>(+) / VCC<br><br>(-) / GND | GP0<br><br>GP1<br><br>GP2<br><br>3V3<br><br>GND | Pin 1<br><br>Pin 2<br><br>Pin 4<br><br>Pin 36<br><br>Common | Menu Rotation A<br><br>Menu Rotation B<br><br>Button Click / Select<br><br>3.3V Power Supply<br><br>Ground / Earth |
| ---                                               | ---                                                       | ---                                             | ---                                                         | ---                                                                                                                |
| **MPU-6050**<br><br>_(Spirit Level / Sismometer)_ | SDA<br><br>SCL<br><br>VCC<br><br>GND                      | GP4<br><br>GP5<br><br>3V3<br><br>GND            | Pin 6<br><br>Pin 7<br><br>Pin 36<br><br>Common              | I2C Data Line<br><br>I2C Clock Line<br><br>3.3V Power Supply<br><br>Ground / Earth                                 |
| ---                                               | ---                                                       | ---                                             | ---                                                         | ---                                                                                                                |
| **HC-SR04**<br><br>_(Distance Sensor)_            | TRIG<br><br>ECHO<br><br>VCC<br><br>GND                    | GP6<br><br>GP7<br><br>VBUS<br><br>GND           | Pin 9<br><br>Pin 10<br><br>Pin 40<br><br>Common             | Trigger Output<br><br>Echo Input<br><br>**5V Power Supply (Important!)**<br><br>Ground / Earth                     |
| ---                                               | ---                                                       | ---                                             | ---                                                         | ---                                                                                                                |
| **Buzzer**<br><br>_(Audio Feedback)_              | (+) Signal<br><br>(-) / GND                               | GP14<br><br>GND                                 | Pin 19<br><br>Common                                        | Signal Input Line<br><br>Ground / Earth                                                                            |
| ---                                               | ---                                                       | ---                                             | ---                                                         | ---                                                                                                                |
| **3W LED Module**<br><br>_(Flashlight)_           | OUT / Signal<br><br>VCC<br><br>GND                        | **GP15**<br><br>VBUS<br><br>GND                 | Pin 20<br><br>Pin 40<br><br>Common                          | Transistor switching line<br><br>**5V High Power Supply**<br><br>Ground / Earth                                    |
| ---                                               | ---                                                       | ---                                             | ---                                                         | ---                                                                                                                |
| **DHT-11**<br><br>_(Temp & Humidity)_             | DATA / OUT<br><br>VCC<br><br>GND                          | GP22<br><br>3V3<br><br>GND                      | Pin 29<br><br>Pin 36<br><br>Common                          | Digital Data Line<br><br>3.3V Power Supply<br><br>Ground / Earth                                                   |
| ---                                               | ---                                                       | ---                                             | ---                                                         | ---                                                                                                                |
| **QRE1113 (IR)**<br><br>_(Hand Gesture Sensor)_   | OUT<br><br>VCC<br><br>GND                                 | GP26<br><br>3V3<br><br>GND                      | Pin 31<br><br>Pin 36<br><br>Common                          | Analog Input (ADC0)<br><br>3.3V Power Supply<br><br>Ground / Earth                                                 |
| ---                                               | ---                                                       | ---                                             | ---                                                         | ---                                                                                                                |

## 4\. Power and UPS System Installation

The power supply architecture allows the device to function seamlessly via a desktop adapter or to operate as a completely cord-free portable device without system interruption:

- **Battery Pack Assembly:** 3 x 18650 lithium-ion cells are wired in series to create a unified pack balancing between 11.1V and 12.6V.
- **BMS Interconnection:** The balance leads of the battery array are soldered sequentially onto the 3S 20A BMS board terminals corresponding to 0V, 4.2V, 8.4V, and 12.6V.
- **Charging Integration:** The output lines of the 3S Type-C charging module are soldered directly to the P+/P- (input/output) terminals of the BMS board. This setup safely facilitates cell recharging using standard smartphone wall bricks.
- **Voltage Regulation:** High-voltage output harvested from the BMS (P+/P-) is piped directly into the input of the 5V 3A Step-Down Buck Converter, dropping it to a regulated, hardware-safe 5V.
- **System Power Delivery:** The clean 5V output line coming from the buck regulator is tied straight to the Raspberry Pi Pico's VBUS (or VSYS) pinout, safely driving the host board and display shield simultaneously.

## 5\. Software Features and Applications

Sense Pi is built around a versatile desktop operating system architecture that coordinates multiple distinct sub-applications through a unified interface layer:

- **Dashboard (Main Screen):** A user-friendly iconic interface layout that ensures smooth application navigation using either the physical rotary encoder dial or the onboard touch controller.
- **Time and Date:** Automatically synchronizes with atomic clock precision over the internet when a network connection is available. If offline, the hardware-driven **RTC (Real Time Clock)** module maintains timekeeping accuracy without interruptions.
- **Live Weather:** Connects to live web resources to stream real-time localized temperature, ambient humidity, and wind speeds, alongside an extended 7-day predictive weather chart layout.
- **Exchange Rates:** Communicates with the Central Bank of the Republic of Turkey (TCMB) data streams to populate live tracking charts for major foreign currencies, including USD, EUR, and GBP.
- **Earthquake Tracker:** Monitors active regional seismic feeds to list current seismic anomalies. It features automated sensory warnings for global tremors exceeding a magnitude of 2.5 on the Richter scale.
- **Smart Alarm Clock:** Offers a custom configuration dashboard for user-defined reminders, wake-up times, and persistent audio notifications.

### Google Calendar Integration (API Script)

Dynamic user schedule parsing is facilitated via a customized Google Apps Script web service deployed at script.google.com. The accompanying doGet(e) script aggregates today's active schedule milestones starting from the query time to midnight, compiling them into clean JSON strings for real-time display rendering on the Sense Pi screen:

function doGet(e) {  
var calendarId = 'primary';  
var now = new Date();  
var endOfDay = new Date();  
endOfDay.setHours(23, 59, 59, 999);  
<br/>var events = CalendarApp.getCalendarById(calendarId).getEvents(now, endOfDay);  
var result = \[\];  
<br/>for (var i = 0; i < events.length; i++) {  
var event = events\[i\];  
var isAllDay = event.isAllDayEvent();  
var startTime = event.getStartTime();  
var timeStr = "";  
<br/>if (isAllDay) {  
timeStr = "All Day";  
} else {  
var hours = startTime.getHours();  
var minutes = startTime.getMinutes();  
timeStr = (hours < 10 ? '0' : '') + hours + ':' + (minutes < 10 ? '0' : '') + minutes;  
}  
<br/>result.push({  
title: event.getTitle(),  
time: timeStr  
});  
}  
<br/>return ContentService.createTextOutput(JSON.stringify(result))  
.setMimeType(ContentService.MimeType.JSON);  
}

### System Control Panel (Settings)

- **Wi-Fi Networking:** Displays active wireless configurations, showing the local assigned IP address and real-time signal quality indicators (RSSI).
- **Storage Diagnostic:** Features graphical charts mapping the memory usage parameters of the onboard Flash file storage ecosystem.
- **Telemetry Monitor:** Tracks continuous machine operating metrics, including system uptime logs and live RAM allocation statistics.
- **UI Customization:** Provides manual sliding scales to dim or brighten screen backlights, alongside an interface toggle to disable or unmute global buzzer tones.

## 6\. Sensors & Tools Hub

All core hardware measurement subroutines and diagnostic testing features are consolidated within a dedicated utilities menu:

| **Application Name**   | **Hardware Dependency** | **Operational Description**                                                                                                                                                  |
| ---------------------- | ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Room Monitor**       | DHT-11                  | Tracks continuous atmospheric conditions, providing real-time ambient heat logs and humidity ratios directly onto the system display.                                        |
| ---                    | ---                     | ---                                                                                                                                                                          |
| **Sismometer**         | MPU-6050                | Evaluates desktop vibrational vectors (G-Force variations) and visualizes mechanical tremors using numeric plotting techniques.                                              |
| ---                    | ---                     | ---                                                                                                                                                                          |
| **Spirit Level**       | MPU-6050                | Measures workspace surface alignment (Pitch and Roll vectors). **The piezo buzzer emits a clear audio beep code immediately upon hitting a perfect horizontal zero vector.** |
| ---                    | ---                     | ---                                                                                                                                                                          |
| **Pedometer**          | MPU-6050                | Counts total physical steps during portable use, mapping approximate mileage statistics alongside metabolic calorie depletion indexes.                                       |
| ---                    | ---                     | ---                                                                                                                                                                          |
| **Distance Meter**     | HC-SR04                 | Calculates exact distances within a 2cm to 400cm working range with laser-like accuracy, cataloging logging history into the system memory.                                  |
| ---                    | ---                     | ---                                                                                                                                                                          |
| **Flashlight (Torch)** | 3W Power LED Module     | When switched to "ON" from the dashboard UI, it passes a current to trigger the high-intensity 3W perimeter LED, casting a powerful throw of light into dark spaces.         |
| ---                    | ---                     | ---                                                                                                                                                                          |

## 7\. Screensaver and Ambient Smart Information Mode

- **Contactless Activation:** By integration of the \*\*QRE1113\*\* infrared reflectance module along the chassis perimeter, the system monitors proximate hand waves. Sensing near-field movement triggers the screen-saver state instantly without needing physical panel contact.
- **Ambient Info Interface:** Upon entering the screensaver phase, the host platform enters a low-power routine, clear of clutter. The display draws an elegant analog clock overlay, current date variables, and minimalist network-updated weather condition graphics beside active temperature data points.

## 8\. Sense Pi V1 - Installation and Setup Guide

This guide provides a step-by-step walkthrough to flash the MicroPython firmware, configure Thonny IDE, and upload the Sense Pi application source code to your Raspberry Pi Pico 2W.

### Step 1: Flashing the MicroPython Firmware (.uf2)

- **Disconnect the cable:** Unplug the USB cable from your computer (ensure the Sense Pi device is powered down).
- **Press and hold BOOTSEL:** Locate the small white button labeled **BOOTSEL** on the Raspberry Pi Pico 2W board. Press and hold it down.
- **Connect the cable:** While holding the BOOTSEL button, plug the USB cable back into your computer.
- **Release the button:** After 2 seconds, release the button. A new removable drive named **"RP2350"** (or RPI-RP2) will appear on your computer.
- **Copy the file:** Drag and drop or copy-paste your RPI_PICO_W-20251209-v1.27.0.uf2 file directly into this new drive. The drive will automatically unmount and close once the flashing process is complete.

### Step 2: Configuring Thonny IDE

- Launch **Thonny IDE** on your computer.
- Click on the interpreter selection menu located at the **bottom-right corner** of the Thonny window.
- Select **"MicroPython (Raspberry Pi Pico)"** from the list. Thonny's terminal (Shell) will refresh and recognize your connected device.

### Step 3: Enabling the File Manager Panel

- In Thonny's top menu bar, click on **View**.
- From the dropdown list, check the option for **Files**.
- Two file browser panels will appear on the left side of your screen:
  - **This Computer (Top Panel):** Displays files stored on your local computer.
  - **Raspberry Pi Pico (Bottom Panel):** Displays files stored on your Pico 2W internal storage.

### Step 4: Uploading Project Files and Folders

- Navigate to your local Sense Pi project directory using the **This Computer** panel.
- Right-click on your project folders (such as the lib library folder, asset folders, and icons) and choose **"Upload to /"**.
- Repeat this for all supporting Python files and asset structures to mirror them onto the Pico's root storage.

### Step 5: Setting Up Auto-Start ([main.py](http://main.py))

- Locate the primary application script that initializes your UI layout (e.g., sensepi.py or app.py).
- Rename this specific startup file to exactly **main.py**.
- Upload this main.py file directly to the root directory of the **Raspberry Pi Pico** panel so it sits on the highest directory level.

### Step 6: Standalone Deployment (UPS Battery Test)

- Click the red **"Stop/Restart backend"** button in Thonny to safely close the active execution connection.
- Safely unplug the USB data cable from your computer.
- Turn on your device's built-in power switch or activate the onboard 3S UPS battery module. The Pico 2W will immediately detect battery voltage, auto-execute your main.py routine, and launch the Sense Pi interface!

##
