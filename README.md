# EspSoftwareSerial

Implementation of the Arduino software serial library for the ESP8266

This fork implements interrupt service routine best practice. Instead of
blocking for whole bytes at a time - voiding any near-realtime
behavior - phase detection and byte assembly is done in the main code.

Except at high bitrates, depending on other activity, this software
serial adapter is fully duplex, if during tx interrupts are enabled.
Please refer to the SoftwareSerial::enableIntTx(...) function.

Same functionality is given as the corresponding AVR library but
several instances can be active at the same time. Speed up to 115200 baud
is supported. The constructor also has an optional input buffer size.

Please note that due to the fact that the ESP always have other activities
ongoing, there will be some inexactness in interrupt timings. This may
lead to bit errors when having heavy data traffic in high baud rates.