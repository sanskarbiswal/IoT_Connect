# IoT-Connect Interface

IoT-Connect is a project to design a hardware unit, which works with multiple sensors and has built-in protocol for data communication.

## Keywords

- **IoT-Socket**    : The actual interface of the system. This is where the sensor is mounted and the RF-communication unit is placed.
- **IoT-Hub**       : The central command node is called the *hub*. This device can either be a MCU-board like Arduino or a computer terminal like a laptop, desktop or even a Raspberry-Pi. 

## Design Scheme

The IoT-Connect device has ports for connection to various sensors.  <br/>
The capacity in the current design is 6-ports for sensors. Majority of the present day sensors have a max. of 5 ports.<br/><br/>
There is additional provision on the PCB to connect to an Arduino to update its firmware.<br/>
The firmware comprises of pin definitions of the socket MCU and the RF trans-communication protocols between the IoT-Socket and IoT-Hub. The sensor will read data and convey it to the MCU which, depending on how it is coded to handle the data, will either run operations with the data, or send the data to the *hub* for processing.<br/>

The *IoT-Socket* will have the following modules:
  - RF module for data trans-ception
  - Microcontroller (MCU) for local processing and control
  - 6-port sensor input
  - 4-port hub connect
  - USB-mini Input port for power

### Power-In Method

Realizing that the device may need power from both battery as well as from AC-mains depending on the configuration of use. 
The choice is based on the following calculations with sources from respective datasheets, available in the *datasheet* directory.<br/>

Components used:
  - MCU => ATtiny85 (300uA in Active Mode)
  - RF Unit => nRF24L01 (12mA in Tx Mode)
  - Sensor => *variable models* (2mA)

The sensor is never active while the RF unit is active. This is to ensure that the multiple connections can be made with the limited number of ports available in the MCU.

Thus, if programmed pragmatically to only transmit data every 1 minute, then using AA-cells with capacity of 2500mAh, we get almost 400 days of battery backed power. If the transmit period is changed to 30s, then the device can be run on the AA-cell setup for 200 days.

However, if the rate of use of the RF module is once very second or once every two seconds, the life-time of use is limited to not more than one day. 

Thus, the mini-USB B type port provides power into the system. The device can thus be powered by either a USB charger or by AA-cell pack which has connection terminating as an USB port.

# System Schematic and PCB design

<img src="imgs\\V_0_1.png"><br/>

<img src="imgs\\V_0_1_PCB.png"><br>

# Working Procss Flow

