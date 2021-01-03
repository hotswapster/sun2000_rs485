# Huawei SUN2000 PV Inverter Interface  

This application allows you to read data from a Huawei Sun2000 Solar Inverter using its built in RS485 port. It returns a JSON object.
In `read.py` comment/uncomment the section appicable to your inverter model.

## NOTICE
This software and instructions are provided as-is without an warrenty, none of this work is endorsed or approved by Huawei, you use this at your own risk. PV Inverters are high power devices if you are at all unsure stop and consult a qualified professional.


## Hardware
You will require a convertor from your computer serial port to RS-485. Tested with:

USB to RS485 DSD Tech SH-U10 which is availble from amazon for around $15 USD
https://www.amazon.com/DSD-TECH-SH-U10-Converter-Compatible/dp/B078X5H8H7

Also tested with the following on a 5KTL inverter:
- QinHeng Electronics HL-340 USB-Serial adapter (~$3 Aliexpress)
- STM485S 232/485 convertor (~$5 from Aliexpress with breakout board)

### 5KTL
#### Wiring
On the communications connector `COM`. Tested and working on all three ports.
|Port|Wiring (pins)|Notes|
|-|-|-|
|1|1, 3, 5|Does not work when WLAN dongle plugged in USB port|
|2|2, 4, 6||
|3|7, 9 6||

Registers taken from "Solar Inverter Modbus Interface Definitions (V3.0)", Document ID: EDOC1100113918, from Huawei Website.

Modbus Slave Address 1. Baud 9600. Often results in error. Unknown reason.

### 12KTL
You will need to connect a RJ45 connector to the RS485-In port of your Sun2000, see page 61 of the User manual for wiring information (http://solar.huawei.com/en-AU/download?p=%2F~%2Fmedia%2FSolar%2Fattachment%2Fpdf%2Feu%2Fservice%2Fdownload%2FSUN2000%208-28KTL%20User%20Manual.pdf)

## Usage
1. Ensure your user is a member off the `dialout` group (Linux).
2. Configure `read.py` by commenting/uncommenting the appropriate registers for you inverter model. Refer comments in file. Configure port and MODBUS address.
3. Ensure dependencies are installed `pip3 install modbusminimal`
4. `python3 read.py [function]` where `[function]` is `newday`, `update`, or `get`

