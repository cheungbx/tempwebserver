/* 
 *  This is the adoption of the original web server developed by Mr. David Bird. Plus additional instructions for beginners added by Billy Cheung.
 *  
 *  
 *  ESP8266 plus WEMOS SHT30-D Sensor with a Temperature and Humidity Web Server
 Automous display of sensor results on a line-chart, gauge view and the ability to export the data via copy/paste for direct input to MS-Excel
 The 'MIT License (MIT) Copyright (c) 2016 by David Bird'. Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated
 documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, 
 distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the
 following conditions: 
   The above copyright ('as annotated') notice and this permission notice shall be included in all copies or substantial portions of the Software and where the
   software use is visible to an end-user.
   THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
   FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHOR OR COPYRIGHT HOLDER BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER 
   LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF, OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
See more at http://www.dsbird.org.uk

*/

/*
 Detailed instructions for beginners Added by Billy Cheung 2019-07-16
======================================================================
This source is adjusted and posted at this github location.

https://github.com/cheungbx/tempwebserver

All credits to the author Mr. David Bird.

Hardware setup
--------------

//    Connect the DHT22  according to the following pin layout.
//    *** WARNING *** Do not swap VCC (+3V) and Ground (0V), otherwised, the chip will be burnt very quickly.
//    ___________
//    |  DHT11  |
//    |    or   |
//    |  DHT22  |
//    |  front  |
//    |  with   |
//    |  holes  |
//    ___________
//      1 2 3 4
//      V D N G
//      C A C N
//      C T   D
//        A

Pin 1-VCC connect to the 3V/VCC of the ESP8266 board
pin 2-Data connect to GPIO 13 (appeared on circuit board of NodeMCU D1 as "MOSI/D7" on NodeMCU D1
Pin 4-GND connect to GND (ground) of the ESP8266 board.
Connect your USB cable from your computer to the ESP8266 board. Make sure you use a good cable. 
Many charging only cable do not have the data pins. 
Long USB cables > 1.5M  may  not work as the data signals dies out due to the long distance.

Software setup
--------------
Adruino->Preference->"Additional Boards Manager Url:", then input http://arduino.esp8266.com/stable/package_esp8266com_index.json
Then exit Arduino and restart to take in the preference.

Reopen Arduino IDE
Tools->Borad:Atmega... ->Boards Manager
Input ESP8266 to search and find the matching board drivers for ESP8266
Click Install to install.

Tools->Borad->LOLIN（Wemos）D1 R2 & Mini (Appear under the section for ESP8266, will not show up unless you did the preference setting above)
Tools->Flash size-> "4M (3M SPIFFS)"  (to partition how much flash memory to store the temperature and humidity data. 3M is the max. 1M is the min.)
Tools->Port:->"/dev/cu......."  - select your serail port used to connect to the ESP8266, if nothing shows up, check your cable or your driver for that USB-Serail port.
                                  Most ESP ports used the CH340 driver (e.g. Wemos D1 R1) or the CP1201 driver.


Reopen Arduino IDE
Tools->Borad->ESP8266 Wemos D1 R1  (Appear under the section for ESP8266, will not show up unless you did the preference setting above)
Tools->Flash size-> "4M (3M SPIFFS)"  (to partition how much flash memory to store the temperature and humidity data. 3M is the max. 1M is the min.)
Tools->Port:->"/dev/cu......."  - your serail port used to connect to the ESP8266, if nothing shows up, check your cable or your driver for that USB-Serail port.
                                  Most ESP ports used the CH340 driver (e.g. Wemos D1 R1) or the CP1201 driver.

File->Open-> open this sketch file (main program source).
Update the credentials.h with your home wifi ssid and passwords

Click tools->Serial Monitor. Set the serial speed to "115200 baud" to  match with this program.
This will allow you to see all the diagnosis messages from the program once the compile and upload is done.
Resize the serial monitor window size and the Arduino IDE size so you can see both on your screen.
On the to right of the Arduino IDE window where the source code is displayed, click "->" to compile and upload.
If you get file not found on files like "??????.h" e.g. NTPClient.h do the following:
Sketch->Include Library->Manage Libraries
at the search box type in the name of the file without the extension, e.g. NTPClient
Select to install the most matching library.
Sometimes you cannot find these missing libraries within the Adruino IDE.
Then you need to search in google and download them fro Github as zip files.
Then click Sketch->Include Library->Add .Zip libraries   and open these zip files to add to the Aruindo IDE.
Then recompile by clicking "->" to compile and upload.

Repeat this process until all missing library files have been instlaled.

Once the program is uploaded, the board will be reset, and you will see diagnosis messages on the serail monitor.
Check that WIFI is connected successfully. If no, check the SSID nad password you put into credentials.h.
You can click the reset button on the ESP8266 board to reboot any time.
Or you can adjust the source code and clieck "->" to recompile and upload again.

Once wifi is successfully connected, you will see the message like th eone below
Connecting to: homewifissid
...........WiFi connected at: 192.168.1.113

Record the ip address.
Then from a PC conneced to the same network as the ESP8266m  open a browser (chrome or i.e.) and browse to the ip address (e.g. 192.168.1.113)
You should see the Web server home page with the charts and the menus.
Click help on the web page to find out how to navigate.


*/
