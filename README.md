# BrightSign

Any BrightSign player **with** a serial port can send and receive commands over serial using a custom script.

This Arduino Library is for use with [BSuControl](https://github.com/zarpli/BSuControl) Script

# Installation & Download

Download the latest version [here](https://github.com/zarpli/BrightSign/archive/refs/heads/main.zip) and put the "BrightSign" folder in your "libraries" folder.

# Basic Usage
```C++
BrightSign BS(Serial1);
```
Instantiate a BrightSign object and attach to Serial1, You may create multiple BrightSign objects.

```C++
BS.update();
```
Read the BrightSign and update its status. This update() function must be called regularly.

```C++
BS.debug();  
```
Enable debug messages on serial port :

|Debug Messages|Description|
|---|---|
|BS : error|The last command was not executed correctly|
|BS : ok|The last command was successful|
|BS : online|The unit starts up and has the script installed|
|BS : media_ended|A file has finished playing|

# Example

Simple example of the BrightSign library that play a media file "demo.mov" locate in "video" directory, and wait for it to finish to run again.
  
The BSuControl Script must be installed in the BrightSign unit memory unit and must be connected to the Serial1 port of the arduino board.  

```C++
#include <BrightSign.h>

// Instantiate a BrightSign object and Attach to Serial1
BrightSign BS(Serial1);   

void setup(){

// Enable debug msg over Serial
BS.debug();               

Serial.begin(9600);
while(!Serial);

Serial.println("Waiting BrightSign Power-Up");
while(!BS.online())BS.update(); 

//Set Volume to 20%
BS.volume(20);            
}

void loop(){
// Update the BrightSign instance
BS.update();
if(BS.media_ended()) BS.play("VIDEO/DEMO.MOV");
}
```

# YouTube

<a href="http://www.youtube.com/watch?feature=player_embedded&v=v_Xolq-GvfM" target="_blank"><img src="http://img.youtube.com/vi/v_Xolq-GvfM/0.jpg" alt="YouTube" width="400" border="10"/></a>
