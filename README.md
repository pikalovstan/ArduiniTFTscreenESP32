#TFT_eSPI Library
This is a TFT graphics library for Arduino processors with performance optimization for STM32, ESP8266 & ESP32. The library is targeted at 32-bit processors. It supports “Four wire” SPI and 8 bit parallel interfaces. The library supports some TFT displays with drivers for ILI9163, ILI9225, ILI9341, ILI9488, ST7735 etc
https://github.com/Bodmer/TFT_eSPI
Frank Boesing has created an extension library for TFT_eSPI that allows a large range of ready-built fonts to be used. Frank's library can be downloaded here. More than 3300 additional Fonts are available here. The TFT_eSPI_ext library contains examples that demonstrate the use of the fonts.

Users of PowerPoint experienced with running macros may be interested in the pptm sketch generator here, this converts graphics and tables drawn in PowerPoint slides into an Arduino sketch that renders the graphics on a 480x320 TFT. This is based on VB macros created by Kris Kasprzak here.

The library contains two new functions for rectangles filled with a horizontal or vertical coloured gradient:

tft.fillRectHGradient(x, y, w, h, color1, color2);

tft.fillRectVGradient(x, y, w, h, color1, color2);

Gradient

The RP2040 8 bit parallel interface uses the PIO. The PIO now manages the "setWindow" and "block fill" actions, releasing the processor for other tasks when areas of the screen are being filled with a colour. The PIO can optionally be used for SPI interface displays if #define RP2040_PIO_SPI is put in the setup file. Touch screens and pixel read operations are not supported when the PIO interface is used. The RP2040 PIO features only work with Earle Philhower's board package, NOT the Arduino Mbed version.

The use of PIO for SPI allows the RP2040 to be over-clocked (up to 250MHz works on my boards) in Earle's board package whilst still maintaining high SPI clock rates.

DMA can now be used with the Raspberry Pi Pico (RP2040) when used with both 8 bit parallel and 16 bit colour SPI displays. See "Bouncy_Circles" sketch.

"Bouncing circles"

Support hase been added for the ESP32 S2 processor variant. A new user setup file has been added as an example setup with an ILI9341 TFT.

The library now supports the Raspberry Pi Pico with both the official Arduino board package and the one provided by Earle Philhower. The setup file "Setup60_RP2040_ILI9341.h" has been used for tests with an ILI9341 display. At the moment only SPI interface displays have been tested. SPI port 0 is the default but SPI port 1 can be specifed in the setup file if those SPI pins are used.

"Rotating cube demo"

Viewports can now be applied to sprites e.g. spr.setViewport(5, 5, 20, 20); so graphics can be restricted to a particular area of the sprite. This operates in the same way as the TFT viewports, see 5. below.

The library now provides a "viewport" capability. See "Viewport_Demo" and "Viewport_graphicstest" examples. When a viewport is defined graphics will only appear within that window. The coordinate datum by default moves to the top left corner of the viewport, but can optionally remain at top left corner of TFT. The GUIslice library will make use of this feature to speed up the rendering of GUI objects (see #769).

The library now supports SSD1963 based screen, this has been tested on a 480x800 screen with an ESP32. The interface is 8 bit parallel only as that controller does not support a SPI interface.

A companion library U8g2_for_TFT_eSPI has been created to allow U8g2 library fonts to be used with TFT_eSPI.

The library now supports SPI DMA transfers for both ESP32 and STM32 processors. The DMA Test examples now work on the ESP32 for SPI displays (excluding RPi type and ILI9488).

TFT_eSPI
TFT_eSPI
An Arduino IDE compatible graphics and fonts library for 32 bit processors. The library is targeted at 32 bit processors, it has been performance optimised for STM32, ESP8266 and ESP32 types. The library can be loaded using the Arduino IDE's Library Manager. Direct Memory Access (DMA) can be used with the ESP32, RP2040 and STM32 processors to improve rendering performance.

Optimised drivers are incorporated for the following processors:

RP2040, e.g. Raspberry Pi Pico
ESP32 and ESP32-S2 (ESP32C3 untested)
ESP8266
STM32F1xx, STM32F2xx, STM32F4xx, STM32F767 (higher RAM processors recommended)
Generic (non-optimised Arduino function calls) are used by the library for other processors.

"Four wire" SPI and 8 bit parallel interfaces are supported. Due to lack of GPIO pins the 8 bit parallel interface is NOT supported on the ESP8266. 8 bit parallel interface TFTs (e.g. UNO format mcufriend shields) can used with the STM32 Nucleo 64/144 range or the UNO format ESP32 (see below for ESP32).

Displays using the following controllers are supported:

ILI9163
ILI9225
ILI9341
ILI9481 (DMA not supported with SPI)
ILI9486 (DMA not supported with SPI)
ILI9488 (DMA not supported with SPI)
HX8357D
S6D02A1
SSD1351
SSD1963
ST7735
ST7789
ST7796
GC9A01
ILI9341 and ST7796 SPI based displays are recommended as starting point for experimenting with this library.

The library supports some TFT displays designed for the Raspberry Pi (RPi) that are based on a ILI9486 or ST7796 driver chip with a 480 x 320 pixel screen. The ILI9486 RPi display must be of the Waveshare design and use a 16 bit serial interface based on the 74HC04, 74HC4040 and 2 x 74HC4094 logic chips. Note that due to design variations between these displays not all RPi displays will work with this library, so purchasing a RPi display of these types solely for use with this library is not recommended.

The "good" RPi displays are the MHS-4.0 inch Display-B type ST7796 and Waveshare 3.5 inch ILI9486 Type C displays are supported and provides good performance. These have a dedicated controller and can be clocked at up to 80MHz with the ESP32 (55MHz with STM32 and 40MHz with ESP8266).

Some displays permit the internal TFT screen RAM to be read, some of the examples use this feature. The TFT_Screen_Capture example allows full screens to be captured and sent to a PC, this is handy to create program documentation.

The library supports Waveshare 2 and 3 colour ePaper displays using full frame buffers. This addition is relatively immature and thus only one example has been provided.

The library includes a "Sprite" class, this enables flicker free updates of complex graphics. Direct writes to the TFT with graphics functions are still available, so existing sketches do not need to be changed.
