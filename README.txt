TelegraphOnTheClock
Telegraph on the Clock is a Arduino Bomb Game in which the buzzer will play a random morse code ranging from the numbeers 0-9 and with the use of the keypad, the player will have to guess what morse code has been outputted by the buzzer. 

##BUILDING AND INSTALLING IT 
  - Get the needed parts (check I.)
  - Connect the components (check II.)
  - If you are not using the Arduino Online Editor, manually install the three included libraries: "Wire.h", "Keypad.h" and "LiquidCrystal_I2C.h". Installing libraries steps: https://www.arduino.cc/en/guide/libraries
  - Although the Arduino IDE downloads it for you so no issues there
  - Else if you are using the Arduino Online Editor, I think those libraries come pre-installed. But let me know if you run into any trouble with this
  - Open the file telegraphontheclock.ino to see the full code and upload it onto your arduino
  - Test the bomb game (check III.)

I. Parts used:
  - Arduino Uno
  - LCD Display 16x2 12C
  - Piezo Buzzer
  - RGB LED Module
  - 4x4 Matrix Membrane Keypad
  - eighteen(18) jumper wires

II. Connections:
  1. Connecting the LCD Display
    - LCD GND connect to Arduino GND
    - LCD VCC connect to Arduino 5V
    - LCD SDA connect to Arduino A4
    - LCD SCL connect to Arduino A5
  2. Connecting the Piezo Buzzer and RGB Module
    - Piezo Buzzer(+) connect to Arduino 10 
    - Piezo Buzzer(-) connect to Arduino GND
    - RGB Red connect to Arduino 11
    - RGB Green connect to Arduino 12
    - RGB Blue connect to Arduino 13
    - RGB GND connect to Arduino GND
  3. Connecting the Keypad
    - check this website for the keypad pin configurations: https://components101.com/misc/4x4-keypad-module-pinout-configuration-features-datasheet
    - R1 connect to Arduino 9
    - R2 connect to Arduino 8
    - R3 connect to Arduino 7
    - R4 connect to Arduino 6
    - C1 connect to Arduino 5
    - C2 connect to Arduino 4
    - C3 connect to Arduino 3
    - C4 connect to Arduino 2

III. How to Use the Bomb Game
  - Make sure to troubleshoot each component and adjust it according to what's wrong, and if you have newer versions of said components, ther might be some minor adjusments
  - Make sure to upload the code onto the Arduino Uno before plugging in the power
  - The game will prompt asking the player to preess # in the keypad to start
  - As you start, the buzzer will sound out a random morse code ranging from 0-9, containing dits(short sound) and dahs(long sound)
  - As the sound is finished, the player can choose a number on the keypad corresponding to the sound played
  - In the LCD Display, it keeps track of the score and lives left for the player, in the main code, it is set to have 3 lives
  - Also, when a sound has been played and you want to restart the game, press # to restart
  - The RGB LED Module also displays different colors of light depending on the status of the game: BLUE-Idle, GREEN-Correct, RED-Incorrect, YELLOW-PlayAgain
  - When all lives have been consumed, the buzzer will sound an explosion sound and the LED will be set to RED for a fixed amount of time
  - When the explosion has ended, it will prompt the user to play again
  - Adjust the code based on your preferences



