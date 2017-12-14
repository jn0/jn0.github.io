# Raspberry Pi -- Microphone and MAX4466 amplifier

## Features

- Maxim MX4466 Op-Amp Amplifier
- Adjustable Gain 25x to 125x
- 20-20KHz electret microphone Pre-Soldered
- Excellent low-noise performance

## etc

- [read it](https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=41885)

```cpp
int readADC(int adcnum, int clockpin, int mosipin, int misopin, int cspin)
{
    int commandout = adcnum;

    bcm2835_gpio_write(cspin, HIGH);
    bcm2835_gpio_write(clockpin, LOW);
    bcm2835_gpio_write(cspin, LOW);
                            
    commandout |= 0x18;
    commandout <<= 3;
                                        
    for(int i = 0; i < 5; i++) {
        if (commandout & 0x80)
            bcm2835_gpio_write(mosipin, HIGH);
        else
            bcm2835_gpio_write(mosipin, LOW);
        commandout <<= 1;
        bcm2835_gpio_write(clockpin, HIGH);
        bcm2835_gpio_write(clockpin, LOW);
    }

    int adcout = 0;

    for(int i = 0; i < 12; i++) {
        bcm2835_gpio_write(clockpin, HIGH);
        bcm2835_gpio_write(clockpin, LOW);
        adcout <<= 1;
        if (bcm2835_gpio_lev(misopin))
            adcout |= 1;
    }

    bcm2835_gpio_write(cspin, HIGH);

    adcout >>= 1;
    return adcout;
}

```

# EOF #
