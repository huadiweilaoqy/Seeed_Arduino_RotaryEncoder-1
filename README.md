# GroveEncoder Library

This library support Encoder.

# Hardware requirements

- Arduino/Genuino UNO
- Grove Shield and a cable
- Grove Rotary Encoder v1.2

## Recommended hardware setup

1. Put the Grove Kit Shield in the Arduino UNO
2. Plug one side of the cable into the D2 port on the Grove Shield
3. Plug the other side of the cable into the Grove Rotary Encoder v1.2
4. You're done!  Power it on and start programming.

# Installation

Download the ZIP and install using the Arduino IDE.  Alternative 
installation instructions may be found [here](https://www.arduino.cc/en/Guide/Libraries).

# Usage

The GroveEncoder library makes it possible to read the value off of an encoder.
When the knob is turned clockwise, the value will increment.  When the knob is
turned counterclockwise, the number will decrement.  This value is a 32 bit
signed integer.

You can use this library via polling, or attach an interrupt handler if you're
an advanced user.  Please see the examples directory.

## Polling

Simply create a GroveEncoder object and pass NULL as the second parameter.

```c
#include <GroveEncoder.h>

void loop() {
  GroveEncoder myEncoder(7, NULL);
  while (1)
  {
    int value = myEncoder.getValue();
    // getValue returns the number currently on the encoder.
    Serial.print(value, HEX);
  }
}
```

## Interrupts

Create a GroveEncoder object and pass it a pin as well as a callback.

```c
#include <GroveEncoder.h>
int value = 0;
int bt_flag = 0;
void myCallback(int newValue, bool flag) {
  if(value != newValue)
  {
    value = newValue;
    Serial.print(newValue, HEX);
    Serial.print("\n");
  }
  if(flag && bt_flag)
  {
    Serial.println("button");
    bt_flag = 0;
  }
}
GroveEncoder myEncoder(2, &myCallback);
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
}

void loop() {
  // put your main code here, to run repeatedly:
  while(1)
  {
    delay(100);
    bt_flag = 1;
  }
}
```

# License

See LICENSE.
