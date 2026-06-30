This project simulates natural daylight using a PWM-controlled LED. It adjusts the LED's brightness to mimic the sun's position:
Platform: WeMos D1 Mini (ESP8266)
Display: 1602 I²C LCD
Input: Button on D4 to toggle LCD pages
Output: PWM LED on D3 to simulate daylight brightness
Location: Cape Town (-33.92490, 18.42410)
API: ipgeolocation.io Astronomy API
________________________________________
 Hardware Behavior
• Button (D4): Cycles between 4 different LCD display pages.
• PWM LED (D3):
o Brightness ramps up gradually from sunrise to solar noon.
o Then dims from noon to sunset, simulating the daylight cycle.
o PWM range: 30 to 255 (never fully off).
________________________________________
 Fetched API Data
Data is pulled every 60 seconds and includes:
• Sunrise time
• Solar noon time
• Sunset time
• Sun altitude
• Moon altitude
• Moon azimuth
• Moon distance
• Date
________________________________________
 LCD Display Pages
Page Line 1 Line 2
Case 0 MoonAz: xxx.x Alt: yy.y D: zzzzzz
Case 1 MoonDist: zzzz km
Case 2 Date: MM-DD Up: 07:30 Set: 17:54
Case 3 Sun Alt: aa.a LED PWM: xxx
These values update live from the internet.
Pages loop automatically with each press of the button.
________________________________________
 PWM LED Brightness Logic
if (sunAltitude  0)
  brightness = map(sunAltitude, 0, 90, 30, 255);
else
  brightness = 0;
• LED is off before sunrise or after sunset.
• At noon (highest sun altitude), the LED is brightest.
• Based on sun's current altitude, not just the time.
