# Using Contiki on Mikro-E Clicker

## Overview

This section explains how to build Contiki code for Mikro-E Clicker and to flash the compiled application image on Mikro-E Clicker.

## Revision History

| revision  | changes from previous revision |
|---------- |------------------------------- |
| 1.0.0     | Initial release                |

## Package Content

Some key paths where IMG have added source code to support Contiki on Mikro-E Clicker:

| Folder              				| Content                                              							                      |
| :----               				| :----                                                							                      |
| platform/mikro-e			      | Porting of drivers for peripherals like Button, LED, CC2520, CA8210 etc. on Mikro-E Clicker			|
| examples/mikro-e            | Applications for Mikro-E Clicker board                                                  |         

## Cascoda ca8210 transceiver support

Cascoda ca8210 transceiver driver has been added git submodule. So you first need to checkout the driver code before building any contiki application based upon ca8210.

    $ git submodule init "dev/ca8210"
    $ git submodule update

## Getting Started

The xc32 compiler version 1.34 from Microchip can be used for compilation of the source code. Download the xc32 compiler from
<a href="http://www.microchip.com/pagehandler/en_us/devtools/mplabxc/">Microchip's website</a> and add tool chain path in the
environment variables and compile an example, say "Hello World" which is included in Contiki as per below:

    $ export PATH=$PATH:/opt/microchip/xc32/v1.34/bin/

Platform mikro-e makefile has been updated to build either for cc2520 or for ca8210 depending the build option USE_CC2520 or USE_CA8210. The application e.g. Hello World can be built for Mikro-E Clicker and HEX file can be generated to flash on the board as per below:

For clicker boards using CA8210:

    $ cd examples/hello-world
    $ make TARGET=mikro-e USE_CA8210=1
    $ /opt/microchip/xc32/v1.34/bin/xc32-bin2hex hello-world.mikro-e

For clicker boards using CC2520:

    $ cd examples/hello-world
    $ make TARGET=mikro-e USE_CC2520=1
    $ /opt/microchip/xc32/v1.34/bin/xc32-bin2hex hello-world.mikro-e
