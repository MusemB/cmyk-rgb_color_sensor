[general](#cmyk-rgb_color_sensor)

[introduction](#introduction)

[General purpose input output (GPIO)](#GPIO)

[MCU header file](#MCUHEADERFILE)

[Serial peripheral interface (SPI)](#SPI)

# cmyk-rgb_color_sensor
the aim of this project is to make a device (based on the stm32 microcontroller), which samples color from real life objects and displays the color's CMYK and rgb values on a lcd screen


## Objectives
1. write drivers for both the sensor & the display from scratch
2. create a gui for the device

## parts
1. STM32F407G-DISCOVERY microcontroller
2. Waveshare 2inch lcd module
3. color sensor (tbd)


## introduction
I decided to create this sensor due to the fact that I'm learning about embedded C, and the usecase aligns with my hobby of painting.



## GPIO


## MCU Header file

##(SPI)
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
* master has to be configured to transmitter mode & slave to receiver mode

#### Simplex communication
* when MOSI is only enabled. i.e master only transmits to slave

### SPI functional block diagram
* The shift register consists of 2 bytes
* Tx buffer is connected to APB bus, which can write to it, and in turn
  Tx buffer writes to the shift register, when the shift register is free (i.e, not used by MISO).
  Afterwards, the data is sent from the shift register to MOSI
  
* Rx buffer reads from the shift register and writes to APB bus
* both Rx and Tx buffers invoke an interrupt when they are full
* master clock is controlled by Baud rate generator

### slave select (NSS) pin management
* when a device is in slave mode, the NSS works as a standard "chip select" input, which lets the slave to communicate with it's master
* in master mode, NSS can be used as either an output or input.
  In input mode, the master's NSS can prevent multi-master bus collision, and in output mode, it can drive a slave select signal to a slave
#### types of slave managements
* software slave management (SSM): when SSM =1, the slave select information (SSI) is driven by the bit value in register SPIx_CR1.
The external NSS is free for use.

* hardware slave management (NSS) pin makes the slave listen to whether the master enables it.
* Master's NSS has to be connected to VDD to avoid errors (or unconfigured)
