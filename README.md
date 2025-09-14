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


##MCU Header file

## serial peripheral interface (SPI)
* serial communication protocol between master and slave devices
* consists of the following pins:
* 1. Serial clock (SCLK) = a clock produced by master, which controls slave's clocks
  2. Master out, slave in (MOSI)= pin, which sends output on master side and takes input on slave side
  3. Master in, slave out (MISO) = pin, which does the converse of MOSI
  4. slave control (SS) == used to select which slaves are active (slave is active when SS is 0)

* SPI is synchronous serial
* max distance = 10ft (3m)
* max speed = fPCLK/2


