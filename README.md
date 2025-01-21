# Flipper Zero hardware modules
This is a collection of PCBs for the various Flipper Zero GPIO expansion modules I've created.

# Modules

| Module                      | Design Completed | Board Tested | Case | Latest Version |
|-----------------------------|------------------|--------------|------|----------------|
| 20W IR Blaster (Simplified) | Yes              | No           | No   | v0.1           |
| 20W IR Blaster              | No               | No           | No   | N/A            |
| EDC-1                       | Yes              | No           | No   | v0.1           |
| ESP-01 Slim                 | Yes              | No           | No   | v0.1           |
| I2C & OneWire Probes        | Yes              | No           | No   | v0.1           |
| IR Blaster Mini             | Yes              | No           | No   | v0.2           |
| RS232 Serial                | Yes              | No           | No   | v0.1           |
| Slim CC1101 & NRF24L01      | Yes              | No           | No   | v0.1           |
## 20W IR Blaster (Simplified)
Highly experimental IR blaster that uses a supercapacitor to store and dump energy, allowing the board to push far more power through the IR LEDs than the Flipper Zero is capable of supplying on its own. By itself, the Flipper can supply up to 1.2A @ 5V and 1.2A @ 3.3V, however, due to battery limitations and SD card corruption risks, in practice it can supply about 5W max. By charging the supercapacitor at less than 5W, the Flipper's power rails never get stressed. The supercapacitor can then be disharged into the IR LEDs, allowing much more powerful bursts, in this case about 20W. The built in IR blaster is on the order of tens of milliwatts, or maybe 200x less powerful. As far as I'm aware, this is the most powerful IR blaster out there that's still powered by the Flipper Zero. 
This simplified version uses a resistor to limit the charge current of the supercapacitor and a comparator to limit the charge voltage to 3.3V. There is an indicator LED on board that shows when the cap is charged enough to fire. 
## 20W IR Blaster
This is the same idea as the simplified version above, but includes some nice features as well.
1. The supercapacitor is charged with a dedicated IC designed for exactly this purpose, meaning it doesn't waste power with resistors, so it burns less battery.
2. Includes temperature protection on the LEDs, meaning it will light up an error LED and refuse to fire if the LEDs are above a certain temperature.
3. Like the simplified version, it has an indicator LED to show when the supercapacitor is charged enough to fire, but it also will refuse to fire if there is not enough charge. 
4. Includes a boost-converter that allows the supercapacitor to charge up to about 7V, enabling two sets of LEDs to be placed in series, potentially doubling the IR output power.
Note: this board design has not yet been completed, so it is still theoretical. Also the name will probably have to change to reflect the actual power once designed.
## EDC-1
This is the first EDC or Every Day Carry board, designed to be small and pack as many useful features in as possible. There are four parts to this board:
1. A \~0.5W flashlight that runs off the 5V rail and uses pin C3 to turn on and off.
2. A Seeedstudio Xiao footprint that can accept several different ESP32 variant board for things like Marauder\*, Ghost ESP\*, WiFi Scanner, flipHTTP, and more. Pins connected are RX, TX, and two GPIO pins for other interactions, such as the module presence check that the WiFi Scanner app uses. The ESP is powered from the 5V rail using its own onboard regulator.
3. A DS18B20 temperature probe connected to pin 10 for quickly getting the ambient air temperature\*\*.
4. A QWIIC connector for attaching I2C peripherals such as environmental sensors or Wii Nunchucks to the flipper. These run on the 3.3V pin, so power hungry devices should be powered externally. 
\* there is no microSD card slot, so functionality may be limited.
\*\* since the sensor is mounted to the PCB, which is also used to dissipate heat from the LEDs and holds the Xiao ESP32, the reading may not be accurate for a while after using the flashlight or ESP. 
## ESP-01 Slim
Very simple module that allows an ESP8266 ESP-01 to be mounted nearly flush with the Flipper Zero for apps such as the WiFi Scanner. The ESP is powered from the 3.3V rail, but there are a few capacitors to help smooth out any current spikes that it might draw, so it should be safe with no risk of SD corruption.
## I2C & OneWire Probes
This board includes one QWIIC connector that can be used for I2C peripherals and three 3.5mm headphone-style jacks that can be used to attach either I2C or OneWire (eg. DS18B20 temperature sensor) devices. The folder shows a couple of example devices, including long waterproof DS18B20 temperature sensor probes, short direct connect SHT35 temperature and humidity sensor probes, and some others. 
## IR Blaster Mini
A much simpler IR blaster than the 20W ones, this uses the more traditional driving method of a simple resistor to set the current and draws power directly from the 5V pin. The output is somewhere around 4W, which is on par with most of the high powered IR blasters on the market currently.
## RS232 Serial
Uses an SP3232 to convert the Flipper Zero's 3.3V TTL UART into true ±10V RS232 signals, which are then presented on both male and female DP9 connectors. These connectors share the same signals, so they cannot be used independently or at the same time. 
## Slim CC1101 & NRF24L01
This is my version of the classic breakout boards that includes a 3.3V regulator, smoothing capacitors, and a footprint for the CC1101 and NRF24L01 radio modules. It actually has two footprints, one for the CC1101 and shorted NRF24L01 modules and one for the longer NRF24L01+PA+LNA modules so it doesn't end up sticking way out over the edge of the Flipper. With some patience, good quality solder, and the plated-hole breakaway board, the modules can be soldered in place without using pins, such that the board sits completely flat against the Flipper, making it very low profile.
