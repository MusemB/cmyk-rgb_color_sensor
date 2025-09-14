# cmyk-rgb_color_sensor
the aim of this project is to make a device (based on the stm32 microcontroller), which samples color from real life objects and displays the color's CMYK and rgb values on a lcd screen


## Objectives
1. write drivers for both the sensor & the display from scratch
2. create a gui for the device

## parts
1. STM32F407G-DISCOVERY microcontroller
2. Waveshare 2inch lcd module
3. color sensor (tbd)


##introduction
I decided to create this sensor due to the fact that I'm learning about embedded C, and the usecase aligns with my hobby of painting.



## General-purpose input output (GPIO)


## MCU Header file

## serial peripheral interface (SPI)
* serial communication protocol between master and slave devices
* consists of the following pins:
* 1. Serial clock (SCLK) = a clock produced by master, which controls slave's clocks
  2. Master out, slave in (MOSI)= pin, which sends output on master side and takes input on slave side
  3. Master in, slave out (MISO) = pin, which does the converse of MOSI
  4. slave control (SS) == used to select which slaves are active (slave is active when SS is 0)

### general spi info:
* SPI is synchronous serial
* max distance = 10ft (3m)
* max speed = fPCLK/2
* behind the scenes, when MOSI and MISO are connected, the LSB of master's shift register gets shifted to the MSB of the
  slave's shift register, while MISO takes the LSB of slave's shift register and shifts it to MSB of master's shift register
* 1 bit from both registers gets transferred per clock cycle (master sends & receives 1 bit per cycle)
* 
### configuration of SPI bus
#### Full-duplex communication:
when MISO & MOSI enabled (default config for SPI)
#### half-duplex communication:
* When MOSI is connected to MISO with a resistor between the data lines (typically 1 kΩ).
* master has to be configged to transmitter mode & slave to receiver mode

