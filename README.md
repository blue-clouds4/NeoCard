# NeoCard
> [!WARNING]
> This is still in its prototyping phase.
<br>
 This is a prototype of a PCB business card <b>under $5</b> in which one can play a game and play a video. The project's complete,the code has no bitmap in it,meaning you have to add your very own bitmap for the animation.

# The things this can do:
- [x] Play a video at 10fps
- [x] Run a game (more on that below)
- [x] Transmit NFC messages
- [x] Look cool

![image](https://github.com/user-attachments/assets/5b3fc10e-1e82-4d7a-95fd-9b008305f782)
![image](https://github.com/user-attachments/assets/94e2b29f-5a3e-4bdc-9da0-cf3e8fd23d45)
![image](https://github.com/user-attachments/assets/ae6bb44b-6eeb-40cb-9b7b-73098d19d64d)
![image](https://github.com/user-attachments/assets/b5111bf2-4a36-4320-aa13-574c7865694c)


<hr>

## The Present Code:

```cpp
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#include <Wire.h>

#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
#define OLED_RESET    -1
#define GAME_BUTTON_PIN    2
#define VIDEO_BUTTON_PIN   1
#define BATTERY_PIN        A0
#define UP_BUTTON_PIN      8
#define DOWN_BUTTON_PIN    9
#define LEFT_BUTTON_PIN    10
#define RIGHT_BUTTON_PIN   11
#define CLOSE_BUTTON_PIN   12

Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

// Game variables
int charX = SCREEN_WIDTH / 2;
int charY = SCREEN_HEIGHT / 2;
String bubbles[] = {
  "Despite everything, it's still you.",
  "What do you seek here, nothing or something? Either way, it's something.",
  "If we die, to die by your side is such a heavenly way to die.",
  "To my mother, farewell. To my father, thank you. To you, the moon.",
  "I dream, but at what cost?",
  "YOU FOUND THE RARE MESSAGE, YOU'RE GOING TO STAR A REPO IN GITHUB.",
  "There is no spoon.",
  "Welcome to the desert of the real.",
  "I know kung fu.",
  "The Matrix has you.",
  "Follow the white rabbit.",
  "Wake up, Neo.",
  "The answer is out there, Neo, and it's looking for you.",
  "I'm trying to free your mind, Neo.",
  "You've been living in a dream world, Neo.",
  "The Matrix is everywhere.",
  "You take the red pill, you stay in Wonderland.",
  "Free your mind.",
  "I can only show you the door. You're the one that has to walk through it.",
  "To deny our own impulses is to deny the very thing that makes us human.",
  "I know why you hardly sleep, why you live alone, and why night after night, you sit by your computer.",
  "A world where anything is possible.",
  "Fate, it seems, is not without a sense of irony.",
  "I believe that, as a species, human beings define their reality through suffering and misery.",
  "Hope. It is the quintessential human delusion, simultaneously the source of your greatest strength and your greatest weakness.",
  "There is no escaping reason; no denying purpose.",
  "Choice. The problem is choice.",
  "Everything begins with choice.",
  "I can feel you now. I know that you're afraid. You're afraid of us. You're afraid of change.",
  "I'm going to show them a world without you. A world without rules and controls, without borders or boundaries. A world where anything is possible.",
  "You're cuter than I thought. I can see why she likes you.",
  "There is no perfect moment, only this one.",
  "We can never see past the choices we don’t understand.",
  "Trinity, I know you can hear me. I'm never letting go. I can't. I just love you too damn much.",
  "You have the look of a man who accepts what he sees because he is expecting to wake up. Ironically, this is not far from the truth.",
  "I believe it is our fate to be here. It is our destiny.",
  "What is real? How do you define real?",
  "You have to let it all go, Neo. Fear, doubt, and disbelief. Free your mind.",
  "Unfortunately, no one can be told what the Matrix is. You have to see it for yourself.",
  "I'm not here to tell you how this is going to end. I'm here to tell you how it's going to begin.",
  "You've felt it your entire life, that there's something wrong with the world.",
  "The Matrix is the world that has been pulled over your eyes to blind you from the truth.",
  "Don't think you are. Know you are.",
  "It's the question that drives us, Neo. It's the question that brought you here.",
  "You think that's air you're breathing now?",
  "Deja vu is usually a glitch in the Matrix. It happens when they change something.",
  "To deny our own impulses is to deny the very thing that makes us human.",
  "There is a difference between knowing the path and walking the path.",
  "I've seen an agent punch through a concrete wall. Men have emptied entire clips at them and hit nothing but air. Yet their strength and their speed are still based in a world that is built on rules. Because of that, they will never be as strong or as fast as you can be.",
  "I'm trying to free your mind, Neo. But I can only show you the door. You're the one that has to walk through it.",
  "No one can be told what the Matrix is. You have to see it for yourself.",
  "There is no spoon.",
  "I didn't say it would be easy. I just said it would be the truth.",
  "I'm not here to tell you how this is going to end. I’m here to tell you how it’s going to begin.",
  "You've been living in a dream world, Neo.",
  "I imagine that right now, you're feeling a bit like Alice. Tumbling down the rabbit hole?",
  "Free your mind.",
  "The Matrix is everywhere. It is all around us.",
  "Unfortunately, no one can be told what the Matrix is. You have to see it for yourself.",
  "It's the question that drives us, Neo. It's the question that brought you here.",
  "You have to let it all go, Neo. Fear, doubt, and disbelief.",
  "I've seen an agent punch through a concrete wall. Men have emptied entire clips at them and hit nothing but air.",
  "The Matrix is a system, Neo. That system is our enemy.",
  "I can feel you now. I know that you're afraid.",
  "To deny our own impulses is to deny the very thing that makes us human.",
  "I know that you're afraid. You're afraid of us. You're afraid of change.",
  "The Matrix is the world that has been pulled over your eyes to blind you from the truth.",
  "It's the question that drives us, Neo. It's the question that brought you here.",
  "You take the blue pill, the story ends. You wake up in your bed and believe whatever you want to believe.",
  "I'm going to show them a world without you. A world without rules and controls, without borders or boundaries.",
  "There is no spoon.",
  "I didn't say it would be easy. I just said it would be the truth.",
  "I know that you're afraid. You're afraid of us. You're afraid of change.",
  "You have to let it all go, Neo. Fear, doubt, and disbelief.",
  "It's the question that drives us, Neo. It's the question that brought you here.",
  "You think that's air you're breathing now?",
  "What is real? How do you define real?",
  "Unfortunately, no one can be told what the Matrix is. You have to see it for yourself.",
  "I'm not here to tell you how this is going to end. I’m here to tell you how it’s going to begin.",
  "You take the red pill, you stay in Wonderland, and I show you how deep the rabbit hole goes.",
  "The Matrix is everywhere. It is all around us.",
  "Deja vu is usually a glitch in the Matrix. It happens when they change something.",
  "You take the blue pill, the story ends.",
  "You take the red pill, you stay in Wonderland.",
  "You have the look of a man who accepts what he sees because he is expecting to wake up.",
  "I'm going to show them a world without you. A world without rules and controls, without borders or boundaries.",
  "You've been living in a dream world, Neo.",
  "The Matrix is the world that has been pulled over your eyes to blind you from the truth."
};
int bubbleX, bubbleY;
int bubbleIndex = 0;
unsigned long lastBubbleTime = 0;
const unsigned long BUBBLE_DELAY = 8000;
bool showRareMessage = false;

enum Mode { SELECTION, GAME, VIDEO };
Mode currentMode = SELECTION;

unsigned long startTime = 0;
bool isMessageDisplayed = false;

/* Commenting out video-related variables and functions
// Video frame variables
const int FRAME_COUNT = 25; // Change this to the number of frames you have
const unsigned char* videoFrames[FRAME_COUNT] = {
  // Add your bitmap frame data here
};
unsigned long lastFrameTime = 0;
const unsigned long FRAME_DELAY = 100; // 100 ms for 10 FPS
*/

const unsigned char borderBitmap[] PROGMEM = {
  0b11111111, 0b11111111, 0b11111111, 
  0b11000000, 0b00000000, 0b00000011, 
  0b11000011, 0b00000000, 0b11000011, 
  0b11000011, 0b11111111, 0b11000011, 
  0b11000000, 0b00000000, 0b00000011, 
  0b11000000, 0b00000000, 0b00000011, 
  0b11000000, 0b00000000, 0b00000011, 
  0b11111111, 0b11111111, 0b11111111
};

void setup() {
  pinMode(GAME_BUTTON_PIN, INPUT_PULLUP);
  pinMode(VIDEO_BUTTON_PIN, INPUT_PULLUP);
  pinMode(BATTERY_PIN, INPUT);
  pinMode(UP_BUTTON_PIN, INPUT_PULLUP);
  pinMode(DOWN_BUTTON_PIN, INPUT_PULLUP);
  pinMode(LEFT_BUTTON_PIN, INPUT_PULLUP);
  pinMode(RIGHT_BUTTON_PIN, INPUT_PULLUP);
  pinMode(CLOSE_BUTTON_PIN, INPUT_PULLUP);
  
  if(!display.begin(SSD1306_I2C_ADDRESS, OLED_RESET)) {
    Serial.println(F("SSD1306 allocation failed"));
    for(;;);
  }
  display.display();
  delay(2000);
  display.clearDisplay();
  display.setTextSize(1);
  display.setTextColor(SSD1306_WHITE);
}

void loop() {
  switch (currentMode) {
    case SELECTION:
      displaySelectionScreen();
      break;
    case GAME:
      displayGame();
      break;
    case VIDEO:
      displayVideo();
      break;
  }
}

void displaySelectionScreen() {
  display.clearDisplay();
  display.setCursor(0, 0);
  display.print(F("Select Mode:"));
  display.setCursor(0, 10);
  display.print(F("1. Game"));
  display.setCursor(0, 20);
  display.print(F("2. Video"));

  display.setCursor(0, 40);
  int batteryStatus = analogRead(BATTERY_PIN) / 10;
  display.print("Battery: ");
  display.print(batteryStatus);
  display.print("%");

  display.display();
  
  if (digitalRead(GAME_BUTTON_PIN) == LOW) {
    delay(100); // Debounce delay
    currentMode = GAME;
  }
  
  if (digitalRead(VIDEO_BUTTON_PIN) == LOW) {
    delay(100); // Debounce delay
    currentMode = VIDEO;
  }
}

void displayGame() {
  // Character movement
  if (digitalRead(UP_BUTTON_PIN) == LOW) {
    charY = max(0, charY - 1);
  }
  if (digitalRead(DOWN_BUTTON_PIN) == LOW) {
    charY = min(SCREEN_HEIGHT - 1, charY + 1);
  }
  if (digitalRead(LEFT_BUTTON_PIN) == LOW) {
    charX = max(0, charX - 1);
  }
  if (digitalRead(RIGHT_BUTTON_PIN) == LOW) {
    charX = min(SCREEN_WIDTH - 1, charX + 1);
  }

  display.clearDisplay();

  // Draw character
  display.fillRect(charX, charY, 2, 2, SSD1306_WHITE);

  // Display text bubble
  if (millis() - lastBubbleTime > BUBBLE_DELAY) {
    bubbleIndex = random(0, sizeof(bubbles) / sizeof(bubbles[0]));
    bubbleX = random(0, SCREEN_WIDTH - 50);
    bubbleY = random(0, SCREEN_HEIGHT - 10);
    lastBubbleTime = millis();
  }

  display.setCursor(bubbleX, bubbleY);
  display.print(bubbles[bubbleIndex]);

  display.display();

  // Exit to selection screen
  if (digitalRead(CLOSE_BUTTON_PIN) == LOW) {
    delay(100); // Debounce delay
    currentMode = SELECTION;
  }
}

void displayVideo() {
  display.clearDisplay();
  display.setCursor(0, 0);
  display.print(F("Video mode is in development..."));
  display.display();

  delay(5000); // 5-second delay
  currentMode = SELECTION;

  /* Commenting out video frame display
  unsigned long currentTime = millis();
  
  if (currentTime - lastFrameTime > FRAME_DELAY) {
    static int frameIndex = 0;
    display.clearDisplay();
    display.drawBitmap(0, 0, videoFrames[frameIndex], SCREEN_WIDTH, SCREEN_HEIGHT, SSD1306_WHITE);
    display.display();
    frameIndex = (frameIndex + 1) % FRAME_COUNT;
    lastFrameTime = currentTime;
  }
  */
}
//the video integration part has its code done,feel free to copy paste the code and use your own bitmap data for the code.I'm planning to integrate my custom monochrome animation,which i'm lazy to integrate now

```
## how the game works:

* its a cube roaming around in void,symbolising neo in the matrix. while he roams,random messages in the interval 8 seconds display a message amoungst 100 messages.
* one of these 100 messages are displayed,this symbolises Morpheus trying to contact neo.
* the matrix has you,and there is nothing you can do,for you're a cube
>i had to come up with a game idea that runs well in a esp-12f and i assume ive assumed what i wanted to do

![image](https://github.com/user-attachments/assets/0f77c556-c21c-48cb-a877-bf346d251d20)
>what it basically does
## how the video part works:
* entered bitmap data cycles constatntly on a fps of 10
> did so because, im afriad that the esp-12f may lag when given the operation to run the video exceeding 10 fps.The video can only be played in monochrome(white and black according to the parts used)
![image](https://github.com/user-attachments/assets/7f594c91-6d9e-495b-9379-7ae118aa5726)
