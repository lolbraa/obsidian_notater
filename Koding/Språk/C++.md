#programmeringsspråk 

# Datatyper
**signed** variables allow both positive and negative numbers, while **unsigned** variables allow only positive values.
- **boolean** (8 bit) - simple logical true/false
- **byte** (8 bit) - unsigned number from 0-255
- **char** (8 bit) - signed number from -128 to 127. The compiler will attempt to interpret this data type as a character in some circumstances, which may yield unexpected results
- **unsigned char** (8 bit) - same as 'byte'; if this is what you're after, you should use 'byte' instead, for reasons of clarity
- **word** (16 bit) - unsigned number from 0-65535
- **unsigned int** (16 bit)- the same as 'word'. Use 'word' instead for clarity and brevity
- **int** (16 bit) - signed number from -32768 to 32767. This is most commonly what you see used for general purpose variables in Arduino example code provided with the IDE
- **unsigned long** (32 bit) - unsigned number from 0-4,294,967,295. The most common usage of this is to store the result of the `millis()` function, which returns the number of milliseconds the current code has been running
- **long** (32 bit) - signed number from -2,147,483,648 to 2,147,483,647
- **float** (32 bit) - signed number from -3.4028235E38 to 3.4028235E38. Floating point on the Arduino is not native; the compiler has to jump through hoops to make it work. If you can avoid it, you should. We'll touch on this later.
![[C++-20240604113106820.jpg]]![[C++-20240604113459936.jpg]]

## Array
### Creating (Declaring) an Array
```C++
// Declare an array of a given length without initializing the values:
int myInts[6];

// Declare an array without explicitely choosing a size (the compiler
// counts the elements and creates an array of the appropriate size):
int myPins[] = {2, 4, 8, 3, 6, 4};

// Declare an array of a given length and initialize its values:
int mySensVals[5] = {2, 4, -8, 3, 2};

// When declaring an array of type char, you'll need to make it longer
// by one element to hold the required the null termination character:
char message[6] = "hello";

int b[ 2 ][ 2 ] = { { 1, 2 }, { 3, 4 } };
```

# Funksjoner

```ARDUINO
returnType functionName(parameterType1 parameter1, parameterType2 parameter2 ...) { // function body here }
```
![[C++-20240604114623060.jpg]]
```
void setup() {
  Serial.begin(9600);
  int x = 2;
  float y = 3.5;
  double z ;

  z = sum(x, y);
  Serial.println(z);

  z = sum(x, 10.1);
  Serial.println(z);

  z = sum(5, 10.1);
  Serial.println(z);
}

void loop() {
}

double sum(int x, float y) {
  double result;

  result = x + y;

  return result;
}
```
# Arduino
## Innebygde konstanter
![[C++-20240604113131133.jpg]]

## Innebygde funksjoner
![[C++-20240604113204206.jpg]]

## Tidsfunksjoner
![[C++-20240604113917245.jpg]]![[C++-20240604113923540.jpg]]


## Serial
### Serial Print
```Arduino
void setup() {
  Serial.begin(9600);
}

// YYYY/MM/DD HH:MM:SS
char buffer[20];
sprintf(buffer, "%i/%02i/%02i %02i:%02i:%02i", Year, Month, Date, Hour, Minute, Second);
Serial.println(buffer);
```

![[C++-20240604113232850.jpg]]

### Serial Read
Serial.readbytes(tabell,5);
- Les antallet byte, lagrar i tabell.

String tekst = Serial.readString();
- Les tekststreng fram til linjeskift
- returnerer tekststreng til programmet

Serial.read() 
- les ascii-verdi
- Tar ein byte ut av serie-bufferet

Serial.parseInt() 
- les talverdi frå seriell kommunikasjon
- parseInt() returns the first valid (long) integer number from the serial buffer. Characters that are not integers (or the minus sign) are skipped.

Serial.parseFloat()
- Som Parseint, men ser etter tal på float-format
- 3.1415926
- 6.02214076e23


## Analog
| Board                             | Operating voltage | Usable pins | Max resolution |
| --------------------------------- | ----------------- | ----------- | -------------- |
| UNO R3                            | 5 Volts           | A0 to A5    | 10 bits        |
| UNO R4 (Minima, WiFi)             | 5 Volts           | A0 to A5    | 14 bits**      |
| Mini                              | 5 Volts           | A0 to A7    | 10 bits        |
| Nano, Nano Every                  | 5 Volts           | A0 to A7    | 10 bits        |
| Nano 33 (IoT, BLE, RP2040, ESP32) | 3.3 Volts         | A0 to A7    | 12 bits**      |

### analogRead(pin)
The analog reading on the pin. Although it is limited to the resolution of the analog to digital converter (0-1023 for 10 bits or 0-4095 for 12 bits). Data type: `int`.
```arduino
int analogPin = A3; // potentiometer wiper (middle terminal) connected to analog pin 3 outside leads to ground and +5V
int val = 0;  // variable to store the value read

void setup() {
  Serial.begin(9600);           //  setup seria

void loop() {
  val = analogRead(analogPin);  // read the input pin
  Serial.println(val);          // debug value
}
```

## Interrupts
### Digital Pins With Interrupts
The first parameter to `attachInterrupt()` is an interrupt number. Normally you should use `digitalPinToInterrupt(pin)` to translate the actual digital pin to the specific interrupt number. For example, if you connect to pin 3, use `digitalPinToInterrupt(3)` as the first parameter to `attachInterrupt()`.

  
| Board                                      | Digital Pins Usable For Interrupts | Notes                                                                                                                                                          |
| ------------------------------------------ | ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Uno Rev3, Nano, Mini, other 328-based      | 2, 3                               |                                                                                                                                                                |
| UNO R4 Minima, UNO R4 WiFi                 | 2, 3                               |                                                                                                                                                                |
| Uno WiFi Rev2, Nano Every                  | All digital pins                   |                                                                                                                                                                |


**Note**  
Inside the attached function, `delay()` won’t work and the value returned by `millis()` will not increment. Serial data received while in the function may be lost. You should declare as `volatile` any variables that you modify within the attached function. See the section on ISRs below for more information.

### Syntax
`attachInterrupt(digitalPinToInterrupt(pin), ISR, mode)` (recommended)  
`attachInterrupt(interrupt, ISR, mode)` (not recommended)  
`attachInterrupt(pin, ISR, mode)` (Not recommended. Additionally, this syntax only works on Arduino SAMD Boards, Uno WiFi Rev2, Due, and 101.)

`interrupt`: the number of the interrupt. Allowed data types: `int`.  
`pin`: the Arduino pin number.  
`ISR`: the ISR to call when the interrupt occurs; this function must take no parameters and return nothing. This function is sometimes referred to as an interrupt service routine.  
`mode`: defines when the interrupt should be triggered. Four constants are predefined as valid values:  
- **LOW** to trigger the interrupt whenever the pin is low,  
- **CHANGE** to trigger the interrupt whenever the pin changes value     
- **RISING** to trigger when the pin goes from low to high,      
- **FALLING** for when the pin goes from high to low.     

```arduino
const byte ledPin = 13;
const byte interruptPin = 2;
volatile byte state = LOW;

void setup() {
  pinMode(ledPin, OUTPUT);
  pinMode(interruptPin, INPUT_PULLUP);
  attachInterrupt(digitalPinToInterrupt(interruptPin), blink, CHANGE);
}

void loop() {
  digitalWrite(ledPin, state);
}

void blink() {
  state = !state;
}
```


## Snippets
### Telle minutter
![[C++-20240603150341720.jpg]]
### Interrupt
![[C++-20240603150313224.jpg]]![[C++-20240604102851477.jpg]]

### Servo følger potentiometer
Mangler output for servomotor (``myservo.attach(pinne)``)
![[C++-20240604102926117.jpg]]
### Servo følger serial read
![[C++-20240604120209674.jpg]]

# CheatSheets
![[C++-20240604112337072.jpg]]
![[C++-20240604112340339.jpg|674]]
![[C++-20240604112337212.jpg]]