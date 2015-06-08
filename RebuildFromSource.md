# Rebuilding Maisforth #

Before the hardware can be rebuilt, the Maisforth ROM needs to be compiled.  [gforth 0.7](http://www.jwdt.com/~paysan/gforth.html) is required to do that.  Go to the maisforth/ directory and type make.

# Rebuilding the hardware #

The hardware synthesis process is currently controlled by a WebPack ISE 10.1 project.  There also is a Makefile based synthesis flow in the source tree, but that procedure does not currently support incremental designs.  Thus, I recommend using the ISE based synthesis process for now.

There are currently two variants of the ISE project, one for my main development board (the Xilinx Spartan 3E starter kit) which lives in the ise/ subdirectory, and one for the Xilinx 3A starter kit.

In order to resynthesize rekonstrukt, load the appropriate project file (ise/rekonstrukt.ise or ise-s3a/rekonstrukt.ise using the ISE project navigator.  Opening the project files should produce no errors.  If it does, please get in touch so that we can work things out.  Then, click on the "my\_system09" node in the upper left pane, which will bring up the "Processes" pane in the middle left.  Right click on "Generate Programming File" and select "Run" from the context menu.

This will regenerate the my\_system09.bit file in the project directory.  The design is partitioned so that when only one part of the design is changed, the other parts will not be resynthesized.  This is a great time saver, as resynthesizing the CPU takes several minutes, and does not usually make sense.

# Rebuilding the usim simulator #

The usim MC6809 simulator is in the usim/ directory.  It can optionally be compiled with a little X11 widget that continuously displays the CPU registers, state and currently accessed memory.  It is known to work on cygwin, MacOS X and FreeBSD.

To build usim without the X11 widget, just type "make" in the usim/ directory.  To include the X11 widget, use "make X11=yes".