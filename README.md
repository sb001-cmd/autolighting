import time
import random

# --------------------------
# Simulated Hardware Classes
# --------------------------

class LDR:
    """
    Simulate an LDR sensor.
    In a real implementation, this would use ADC hardware (e.g., via MicroPython's machine.ADC).
    """
    def __init__(self, pin):
        self.pin = pin

    def read(self):
        # Simulate reading an analog value (0 to 4095 for a 12-bit ADC)
        return random.randint(0, 4095)


class Relay:
    """
    Simulate a relay (e.g., controlling a street light).
    In a real system, this would control a digital output pin.
    """
    def __init__(self, pin):
        self.pin = pin
        self.state = False  # False means OFF, True means ON

    def on(self):
        self.state = True

    def off(self):
        self.state = False

    def get_state(self):
        return "ON" if self.state else "OFF"


class LoRa:
    """
    Simulate a LoRa radio.
    In an actual implementation, you would initialize the LoRa radio with the proper frequency and parameters.
    """
    def __init__(self, frequency):
        self.frequency = frequency
        print(f"LoRa initialized successfully on {frequency} Hz!")

    def send(self, message):
        # Simulate sending a packet via LoRa
        print(f"Data sent via LoRa: {message}")


# --------------------------
# Configuration and Setup
# --------------------------

# Pin definitions (for simulation purposes only)
LDR_PIN = 34
RELAY_PIN = 4

# Thresholds (adjust these based on your calibration)
darkThreshold = 1000   # When the reading is above this, it is considered dark.
brightThreshold = 500  # When the reading is below this, it is considered bright.

# Initialize our simulated components
ldr = LDR(LDR_PIN)
relay = Relay(RELAY_PIN)
lora = LoRa(915e6)  # Use 915E6 (or 915e6) for USA; adjust for your region if needed.

# --------------------------
# Main Loop
# --------------------------

while True:
    # Read LDR sensor value
    ldr_value = ldr.read()
    print(f"LDR Value: {ldr_value}")

    # Control the street light based on the LDR value:
    if ldr_value > darkThreshold:
        relay.on()  # Turn ON the street light
        print("Street Light: ON")
    elif ldr_value < brightThreshold:
        relay.off()  # Turn OFF the street light
        print("Street Light: OFF")
    # (If the LDR value is between the two thresholds, the relay state remains unchanged.)

    # Prepare the message to send via LoRa
    message = f"LDR:{ldr_value},Light:{relay.get_state()}"
    lora.send(message)

    # Wait for 1 second before the next reading (simulate delay for stability)
    time.sleep(1)
