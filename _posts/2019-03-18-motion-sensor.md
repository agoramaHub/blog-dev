---
title: Sensor IoT Workshop - Motion
date: 2019-03-18 12:30:00 Z
categories:
- education
tags: IoT raspberry-pi
layout: post
thumbnail: "/images/motion-sensor.jpg"
excerpt: Working with RPI and Motion Sensors
---

# MOTION SENSOR

![alt text](/images/rpizero.jpg)
![alt text](/images/motion-sensor.jpg)


## Minimal Set-up

![alt text](/images/pir1.jpg)
![alt text](/images/pir2.jpg)
For many basic projects or products that need to detect when a person has left or entered the area, or has approached, PIR sensors are great. They are low power and low cost, pretty rugged, have a wide lens range, and are easy to interface with. Note that PIRs won't tell you how many people are around or how close they are to the sensor, the lens is often fixed to a certain sweep and distance (although it can be hacked somewhere) and they are also sometimes set off by housepets. Experimentation is key!

Ground - Ground
5v on rpi to - 5v on Sensor
Gpio11 - Analogue in

![alt text](/images/motion-sensor-pic-small.jpg)

![alt text](/images/gpio-pizero.png)

This python script will read from GPIO pin 11 and print the input to the Terminal
Copy the code below and save the file on your rpi 'motion-sensor-test.py'
```
import RPi.GPIO as GPIO
import time
GPIO.setwarnings(False)
GPIO.setmode(GPIO.BCM)
GPIO.setup(11, GPIO.IN)         #Read output from PIR motion sensor
while True:
        i=GPIO.input(11)
        print i
        time.sleep(1)

```

Once we are logged into the Raspberry Pi using SSH we can run the script with the command
```
$ sudo python motion-sensor-test.py
```

To do -
Consider adding an LED to turn on when the motion sensor is activated

refs
[Adafruit Guide](https://learn.adafruit.com/pir-passive-infrared-proximity-motion-sensor?view=all)
[Maker Pro Tutorial](https://maker.pro/raspberry-pi/tutorial/how-to-interface-a-pir-motion-sensor-with-raspberry-pi-gpio)



![alt text](/images/terminal-commands.png)
