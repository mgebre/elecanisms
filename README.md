master
======

Master repository for ENGR3199 includes C and Python source code and supporting files

To run the blink code on the Elecanism board, I followed the following steps:
1) I installed the follwing software in this order: MPLAB XC16 -> SCons (after downloading python 2.7 and making sure it is in the right path) -> Bootloadergui
While installing these in Windows I hit a few obstacles. First, I had to fix the advanced settings on my Windows 8.1 such that unsigned programs like the bootloader.
I was also not able to downlaod SCons from the exe file directly so I had to download the zip file and then extract it.

2) I connected the Elecanisms board to my computer and updated the driver from the right folder in my elecanims repo.
Here, I made the mistake of assigning the wrong driver to the board and had to uninstalling before finding the right driver to replace it with. 

3) I followed the command window to call the correct directory (blink), used scons to convert the blink.c file to blink.hex, and I opened the bootloadergui.py application to import, write and run the blink code.


C source code:
#include <p24FJ128GB206.h>
#include "config.h"
#include "common.h"
#include "ui.h"
#include "timer.h"

int16_t main(void) {
    init_clock();
    init_ui();
    init_timer();

    led_on(&led1);
    timer_setPeriod(&timer2, 0.5);
    timer_start(&timer2);

    while (1) {
        if (timer_flag(&timer2)) {
            timer_lower(&timer2);
            led_toggle(&led1);
        }
        led_write(&led2, !sw_read(&sw2));
        led_write(&led3, !sw_read(&sw3));
    }
}

