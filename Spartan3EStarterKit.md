These devices of the [Spartan-3E Starter Kit](http://www.xilinx.com/products/devkits/HW-SPAR3E-SK-US-G.htm) are currently supported:

  * Serial port (fixed at 19200 bps, 8n1)
  * PS/2 Keyboard
  * VGA
  * Switches/Buttons/Encoder/LEDs
  * LCD
  * System SPI bus, serial flash is tested, ADC and DAC not yet done

I had plans to move the Maisforth kernel into the parallel NOR flash and directly execute from there instead of using precious block RAM for ROM.  Presently, only one RAM block of the 20 blocks present in the XC3S500E is free:  8 blocks are occupied by the ROM, 8 are genuine Maisforth RAM and 3 blocks are used by the VDU.  When reading the board documentation carefully, I found out that the NOR flash has its data bit 0 shared with the SPI bus, so it is not possible to transfer data over SPI and access the NOR flash at the same time.  How annoying is that?  I guess the reason for this wiring is mandated by the possibilty of booting the FPGA from the parallel flash, yet it is very annoying and dampened my desire to attempt fully supporting the S3E SK by Maisforth.