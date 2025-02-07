In this project, i have developed an automatic street lighting system. The hardware requirements are below:
Microcontroller__ESP32(preferred for long-range communication)
LDR Sensor
Relay Module
LoRa Module(it controls system upto range more than 1km)
Power Supply( Input: 220V AC (for street light power);Output: 5V/12V DC (for microcontroller and relay) )
LED

WORKING:
LDR Sensor: Measures ambient light levels and sends analog data to the microcontroller.
Microcontrollers:Reads the LDR value,Compares it with predefined thresholds (darkThreshold and brightThreshold)and Activates/deactivates the relay to control the street light.
LoRa Module sends real-time data (LDR value and light status) to a remote receiver (up to 1 km or more).
Relay Module switches the street light ON/OFF based on the microcontroller's output.
