
Source: http://www.gammon.com.au/forum/?id=12625

# Pre-processor problems

On the Arduino forum we get a steady stream of complaints that "valid C" (or "valid C++") does not compile under the Arduino IDE (Integrated Development Environment).

## Example 1
```cpp
typedef void (*GeneralMessageFunction) ();
void checkPin (const int pin, GeneralMessageFunction response)
  {
  } 

void setup () { }
void loop () { }
```

Error:

```
sketch_oct11a:2: error: ‘GeneralMessageFunction’ has not been declared
```

## Example 2:
```cpp
template <typename T> T minimum (T a, T b) 
  {
  if (a < b)
    return a;
  return b;
  }  // end of minimum

void setup () 
  { 
  int foo = minimum (6, 7);
  }
void loop () { }
```

Error:

```
sketch_oct11a:2: error: ‘T’ does not name a type
```


## Example 3:

```cpp
void setup() { }
void loop() { }

#if 0
foo bar ()
{
}
#endif 
```

Error:

```
sketch_oct11a:4: error: ‘foo’ does not name a type
```



In each case the error is caused by the IDE attempting to generate function prototypes for you, and failing to do it properly. In the case of ## Example 3 it generated:


#line 1 "sketch_oct10d.ino"
#include "Arduino.h"
void setup();
void loop();
foo bar ();     // <-------------- problem line (line 4)
#line 1
void setup() { }
void loop() { }

#if 0
foo bar ()
{
}
#endif


However it should not have done so because the function "bar" is inside an #if 0 ... #endif block.

How to avoid this problem?


The solution is simple: Leave your main .ino file empty! Yes, that's it.

Make your "sketch" file empty, like this:

foo.ino:





Then use the IDE to make a new "tab" (down-pointing arrow in the top RH side of the window). Name this something sensible (like sketch.cpp). It has to be a .cpp file, eg.

sketch.cpp:


#include <Arduino.h>

// put your sketch here ...

void setup ()
  {

  }  // end of setup

void loop ()
  {

  }  // end of loop



Now, all of the above ## Examples compile fine! Any .cpp files in the project are not subject to this "function prototype generation" procedure, and thus do not fail under certain circumstances.

Four important details


First, you need to have this line at the start of your .cpp file:


#include <Arduino.h>


That gives you prototypes for all of the Arduino functions (eg. digitalWrite etc.).

Second, if you use libraries (eg. Wire, SPI, EEPROM) then the #include lines for those libraries must go into the main sketch (in addition to any place you would normally put them), or you will get linker errors. This is because the IDE scans your main sketch file (and not the other files) to see which library files need to be included in the compilation. So you can regard your .ino file as a sort-of "Project" file which simply lists what libraries you are using.

So an ## Example .ino file would be:

foo.ino:


#include <Wire.h>
#include <SPI.h>
#include <EEPROM.h>


Now the IDE knows to copy (and compile) those libraries as part of your project. Note that you can still omit any code from the .ino file, just list the libraries you are using.

Third, you can't name the .ino file with exactly the same name as the .cpp file or the IDE will complain. Make them have different names. In other words, you can't have foo.ino and foo.cpp.

Fourth, don't name your main file "main.cpp" as there already is a main.cpp file used by the IDE. (This implements the "main" function which calls setup and loop).


You can get rid of setup() and loop()


Also, if you don't like the setup / loop paradigm, you can go back to just using "main" like this:


#include <Arduino.h>

int main ()
  {
  init ();  // initialize timers
  Serial.begin (115200);
  Serial.println ("Hello, world");
  Serial.flush (); // let serial printing finish
  }  // end of main


A couple of traps there:


Call init() if you want to use things like millis(), micros(), and delay(), because that is where the hardware timers get initialized. This will also affect analogRead(), analogWrite(), and a few other things. Unless you know what you are doing, it is best to call init().

Call Serial.flush() when you are done (as shown) if you have been doing serial printing, otherwise interrupts will be turned off and the most recent serial prints may not be shown.


Also, on boards like the Arduino Leonardo / Micro / Esplora / Robot (boards based on the ATmega32u4 chip) you need to initialize the USB interface after calling init():


#if defined(USBCON)
	USBDevice.attach();
#endif