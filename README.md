# How to take an Earth selfie ?

### Abstract
**What we call Earth selfie is an image taking from an earth observation (EO) satellite closed to our position. Would you like to make it for less than 50$? In this tutorial, we will explain in detail how to build a DIY performed antenna (hardware) and how to obtain a clear image after decoding the incoming signal (software). This tutorial will explain to you the technology behind the radio waves as below.**
<p align="center">
  <img src=https://github.com/wimausberlin/noaa-satellites/blob/main/antenna.gif alt=animated>
</p>

### Context
Electromagnetic waves were, are, and will be all around us. Nowadays, more and more devices generate waves. It can be for example radio waves coming from satellites, microwaves or X-ray waves. The nice part of the radio waves is that they can be easily read with just an antenna and a software-defined radio (SDR). This tutorial will especially work with the NOAA satellites (transmitting APT weather pictures in the frequency range of 137-138 MHz). These spacecraft were for the first time launched more than 40 years ago. They are still in space and send data! The only question now is how to collect and treat them properly?

# Hardware
In this part, we show the different types of antennas more or less advanced and how to built them. The only materials that you will need are as follows:

### Materials
- Aluminium cable (1m50)
- Stick of wood
- Chock block
- Coaxial cable (one end stripped & one end SMA male)
- Coaxial cable (SMA female & RP-SMA male)
- Dongle SDR RTL 3V (2832U)
- Computer on Linux

## Antennas
Any conductor can serve as an antenna. Conductors are sensibles to the magnetic fields and convert the electromagnetic waves (that hold the signal) into a voltage which can be interpretable thanks to a SDR that make the required transformation. 

There are various types of antennas that have different characteristics according to the need of signal reception [[1]](#1). They transform radio waves into electrical signal and vice versa. In this tutorial, we will only listen to radio waves in the purpose to observe the Earth from a satellite.

### V-dipole antenna
The most simpliest antenna that you can create is the V-dipole. You just have to take two aluminium rods connected to a choc block in order to obtain a "V-shape". You bend the dipole legs to create a 120° angle.
For the length of the rod, it is importent to know the dipole length. The classic formula for calculation of the length of a half-wavelength dipole:
  $$
 L=0.5k \frac{c}{f}
$$
  where $k$ is the k-factor (close to 1), $c$ the speed of light and $f$ your frequency.
>  **Note** The length of the each leg should include the connecting wire's length up tothe coaxial connector or coax. Keep this length as short as possible but it will be difficultto stay bellow 1.5 cm.

### Helical antenna
Hell yeah

### Double cross antenna
A great antenna with good efficiency for low elevations and omnidirectional capabilities without requiring a rotor.[[3]](#3)

## Software Defined Radio (SDR)
A SDR system is a configurable radiocommunication system that is performing many hardware protocols such as amplification, fitltering, analog/digital conversions, encryption or network routing. In our experience, the SDR permits to convert the Radio frequencies directly into an output signal, usable by our computer. This is notably thanks to the SDR that we can choose the frequencies we want to receive. 
A SDR is composed of an hardware and software part. The software that we will use with our hardware SDR is called GQRW that we will see on the next part of this tutorial.

# Software
The basic 3 packages you need to record a transmission and obtain an image !

- Satellite tracking software : *sudo apt update && sudo apt install gpredict*
- Define Radio Receiver Software : [GQRX](https://gqrx.dk/download/install-ubuntu), work on linux (use SDR Sharp for Windows)
- Audio to image conversion software : [NOAA-APT](https://github.com/martinber/noaa-apt/releases/download/v1.3.0/noaa-apt_1.3.0-1_amd64.deb)

## Gpredict
Gpredict is a software that permits to track the satellite position in real-time and know in advance when the satellites that we are tracking will pass over our geographic region. We can also connect Gpredict to our Define Receiver Software in order to adjust in real-time our SDR network frequencies, to lower the Doppler effect.

## GQRX
GQRX is an open source software defined radio receiver for linux, with a network/frequency routing GUI. With GQRX, we will record a .wav folder from the satellites signal, that contains Earth picture data transmitted by APT (Automatic Picture Transmission). 

# How information travels wirelessly
The information transmission is possible thanks to the propagation of the waves. For example, Wi-fi, radio, cell-phones use electromagnetic waves to transport data wirelessly. The signal that contains data is in fact just a long succession of 0 and 1. But how the wave by itself transmits this binary signal?

Two mains things that describe a wave are **amplitude** and **frequency**. These 2 concepts serve to transmit information : depending on their variations along the wave, we can interpretate if a bit is currently in a 0 or 1 position :

<p align="center">
  <img src=https://www.5gtechnologyworld.com/wp-content/uploads/2020/02/DigitalMod_pt1_fig1_Digital_modulation_waveforms_659x601.jpg.png>
</p>

# How Doppler effect affect our signal reception
Doppler effect is the frequency variation of a wave, produced by the movement of the source or observer between eachother. Let's see on a satellite how works the Doppler effect:
<p align="center">
  <img src=http://maythenetforcebewithyou.weebly.com/uploads/2/5/8/9/25893902/9875947_orig.gif>
</p>

Let's state that the blue point represents the satellites. This drawing represent then at a non-respected scale the impact of the satellite movement on the electromagnetic wave that it produces.

For example, NOAA-19 satellite move at a speed of 7.43*10³ m.s⁻¹. After a few calculs implying its frequency emission and the light speed, we found that from the receiver point of view, the frequency variation during a passage of the satellite above us is around 6800 Hz. When we kwow that with our SDR software we record in average a range of 15 000 Hz, we then deduce that the 6 800 Hz caused by Doppler effect is signifiant on the quality of the radio that we receive.

# References

<a  id="1">[1]</a> Khan, Abdul & Bilal, Anas. (2016). Various Types of Antenna with Respect to their Applications: A Review.

<a  id="2">[2]</a> Adam, Greger (2019). DIY 137 MHz APT Weather satellite antenna – Or, do we need a circular polarization?

<a  id="3">[3]</a> BLANCO GUTIERREZ, Andrea (2015). 2014 Reception of weather images, [Choice and design / Version 18](https://sourceforge.isae.fr/projects/reception-of-weather-images/wiki/_Choice_and_design/18)

