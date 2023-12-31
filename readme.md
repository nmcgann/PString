# PString V3.0

**Arduino PString Library**

This is the lightweight string class from http://arduiniana.org/%20libraries/pstring/ by Mikal Hart.

***The page says:***

### A Lightweight String Class for Formatting Text

*** Note: PString 3 is now Arduino 1.0 compatible.***

Since Print was introduced with Arduino 0012, several classes, including HardwareSerial, LiquidCrystal, Ethernet Client/Server, and my own NewSoftSerial, have been written to leverage its text rendering engine.  But getting formatted text to output devices not in this short list still requires either writing custom code or turning to expensive alternative solutions like sprintf().

**PString** (“Print-to-String”) is a new lightweight Print-derivative string class that renders text into a character buffer. With PStrings, you can use the Print renderer for any device, even those that do not directly support Print-style text formatting, by first “printing” to a string.

In its simplest use case, you deploy an “on-the-fly” constructor to format text:
```
char buffer[30];
#define pi 3.14159
PString(buffer, sizeof(buffer), pi);
```
This code uses Print’s float rendering functions to generate the string equivalent of pi into buffer.

Since **PString** inherits from Print, PString objects can do everything that other Print-derived classes do:
```	
char buffer[50];
PString mystring(buffer, sizeof(buffer));
char name[] = "Joe";
int age = 45;
 
mystring.print("Hi, my name is ");
mystring.print(name);
mystring.print(" and I am ");
mystring.print(age);
mystring.println(" years old.");
```
This generates the expected sentence in buffer the same as if you had printed to the Serial port.

**Other member functions**

PString is a fairly minimal string class. It can report its length and capacity and give const access to its internal string buffer:

```
Serial.print(str.length());
Serial.print(str.capacity());
Serial.print(str);
```

You can reuse a string by calling its begin() function. This effectively resets the position in the buffer where the next **printed** text will go:

```
str.print("Hello");
str.begin();
str.print("World");
// str contains "World" here
```

**Operators**

PString provides three operators for assignment, concatenation, and equivalency test:

```
char buffer[20];
PString str(buffer, sizeof(buffer));
str = "Yin"; // assignment
str += " Yang"; // concatenation
if (str == "Yin Yang") // comparison
{
  Serial.println("They are equal!");
}
```

**Runtime safety**

PStrings do not “own” their own buffers. Instead, they rely on preallocated static buffers that are passed in at the point of construction. PStrings never allocate memory dynamically, even when the result of a print(), assignment, or concatenation operation would seem to exceed the current buffer’s size. In these cases, the excess data is simply discarded and the string correctly terminated.

Because of these constraints, PStrings can make three key guarantees:

- they will never cause a buffer overflow
- a string’s buffer will always be valid memory, i.e. the original buffer
- buffers will always contain valid (i.e. NULL-terminated) C string data.

**Download**

The latest version of PString is PString3.zip.
Revision History

Version 1 – initial release

Version 2 – include support for inline renderings with modifiers HEX, OCT, etc. (and eventually float precision)

Version 3 – Arduino 1.0 compatibility

**Resource Consumption**

PString objects consume 8 bytes of memory during their lifetimes. Depending on what features are used, #including the PString library usually adds only 100-600 bytes to a program’s size.

All input is appreciated.

Mikal Hart


