/*
 * Project 1: Social Un-distancing
 * By Ellie Huang & Nooshin Mohtashami
 * DIGF-3010-001 - Advanced Wearable Course
 * OCAD University
 * Created on Feb 6, 2022
 * Music  Dart Vader theme (Imperial March) - Star wars 
 * Score: https://musescore.com/user/202909/scores/1141521
 * Music We Wish You a Merry Christmas
 * Score available at https://musescore.com/user/6208766/scores/1497501
*/


#include <Adafruit_CircuitPlayground.h>

int ETseconds = 5000; //  miliseconds before colors start changing 
// the colors
unsigned long Color1 = 0xFF0000;     // red
unsigned long Color2 = 0xF73772; //pink/purple
unsigned long Color3 = 0xFFFF00; //green/yellow
unsigned long Color4 = 0x000000;  //dark/off

unsigned long White = 0xFFFFFF;

//sensor ETButton
int ETButton; 

int ETcounter = 0;
int Upperlimit = 10; //10 LEDs
unsigned long StartTime;
boolean MusicMode = false; // music alternates between happy & star wars

//////////// MUSIC Constants ///////

#define NOTE_B0  31
#define NOTE_C1  33
#define NOTE_CS1 35
#define NOTE_D1  37
#define NOTE_DS1 39
#define NOTE_E1  41
#define NOTE_F1  44
#define NOTE_FS1 46
#define NOTE_G1  49
#define NOTE_GS1 52
#define NOTE_A1  55
#define NOTE_AS1 58
#define NOTE_B1  62
#define NOTE_C2  65
#define NOTE_CS2 69
#define NOTE_D2  73
#define NOTE_DS2 78
#define NOTE_E2  82
#define NOTE_F2  87
#define NOTE_FS2 93
#define NOTE_G2  98
#define NOTE_GS2 104
#define NOTE_A2  110
#define NOTE_AS2 117
#define NOTE_B2  123
#define NOTE_C3  131
#define NOTE_CS3 139
#define NOTE_D3  147
#define NOTE_DS3 156
#define NOTE_E3  165
#define NOTE_F3  175
#define NOTE_FS3 185
#define NOTE_G3  196
#define NOTE_GS3 208
#define NOTE_A3  220
#define NOTE_AS3 233
#define NOTE_B3  247
#define NOTE_C4  262
#define NOTE_CS4 277
#define NOTE_D4  294
#define NOTE_DS4 311
#define NOTE_E4  330
#define NOTE_F4  349
#define NOTE_FS4 370
#define NOTE_G4  392
#define NOTE_GS4 415
#define NOTE_A4  440
#define NOTE_AS4 466
#define NOTE_B4  494
#define NOTE_C5  523
#define NOTE_CS5 554
#define NOTE_D5  587
#define NOTE_DS5 622
#define NOTE_E5  659
#define NOTE_F5  698
#define NOTE_FS5 740
#define NOTE_G5  784
#define NOTE_GS5 831
#define NOTE_A5  880
#define NOTE_AS5 932
#define NOTE_B5  988
#define NOTE_C6  1047
#define NOTE_CS6 1109
#define NOTE_D6  1175
#define NOTE_DS6 1245
#define NOTE_E6  1319
#define NOTE_F6  1397
#define NOTE_FS6 1480
#define NOTE_G6  1568
#define NOTE_GS6 1661
#define NOTE_A6  1760
#define NOTE_AS6 1865
#define NOTE_B6  1976
#define NOTE_C7  2093
#define NOTE_CS7 2217
#define NOTE_D7  2349
#define NOTE_DS7 2489
#define NOTE_E7  2637
#define NOTE_F7  2794
#define NOTE_FS7 2960
#define NOTE_G7  3136
#define NOTE_GS7 3322
#define NOTE_A7  3520
#define NOTE_AS7 3729
#define NOTE_B7  3951
#define NOTE_C8  4186
#define NOTE_CS8 4435
#define NOTE_D8  4699
#define NOTE_DS8 4978
#define REST      0


// change this to make the song slower or faster
int tempo = 108;

// change this to whichever pin you want to use
int buzzer = 11;

// notes of the moledy followed by the duration.
// a 4 means a quarter note, 8 an eighteenth , 16 sixteenth, so on
// !!negative numbers are used to represent dotted notes,
// so -4 means a dotted quarter note, that is, a quarter plus an eighteenth!!
int melody[] = {
  
  // Dart Vader theme (Imperial March) - Star wars 
  // Score: https://musescore.com/user/202909/scores/1141521
  
  NOTE_AS4,8, NOTE_AS4,8, NOTE_AS4,8,//1
  NOTE_F5,2, NOTE_C6,2,
  NOTE_AS5,8, NOTE_A5,8, NOTE_G5,8, NOTE_F6,2, NOTE_C6,4,  
  NOTE_AS5,8, NOTE_A5,8, NOTE_G5,8, NOTE_F6,2, NOTE_C6,4,  
  NOTE_AS5,8, NOTE_A5,8, NOTE_AS5,8, NOTE_G5,2,
  
  
};

int melody1[] = {

  // We Wish You a Merry Christmas
  // Score available at https://musescore.com/user/6208766/scores/1497501
  
  NOTE_C5,4, //1
  NOTE_F5,4, NOTE_F5,8, NOTE_G5,8, NOTE_F5,8, NOTE_E5,8,
  NOTE_D5,4, NOTE_D5,4, NOTE_D5,4,
  NOTE_G5,4, NOTE_G5,8, NOTE_A5,8, NOTE_G5,8, NOTE_F5,8,
  NOTE_E5,4, NOTE_C5,4, NOTE_C5,4,
  NOTE_A5,4, NOTE_A5,8, NOTE_AS5,8, NOTE_A5,8, NOTE_G5,8,
  NOTE_F5,4, NOTE_D5,4, NOTE_C5,8, NOTE_C5,8,
  NOTE_D5,4, NOTE_G5,4, NOTE_E5,4,
  NOTE_F5,2, 


};
// sizeof gives the number of bytes, each int value is composed of two bytes (16 bits)
// there are two values per note (pitch and duration), so for each note there are four bytes

int notes = sizeof(melody) / sizeof(melody[0]) / 2;
int notes1 = sizeof(melody1) / sizeof(melody1[0]) / 2;

// this calculates the duration of a whole note in ms
int wholenote = (60000 * 4) / tempo;

int divider = 0, noteDuration = 0;


//// MUSIC ////


void setup() {
  CircuitPlayground.begin();
  CircuitPlayground.clearPixels();
  CircuitPlayground.setBrightness(2);
  //set the input
  pinMode(3, INPUT);
}

void loop() {
  // read input
  ETButton = digitalRead(3);
  if (ETButton) {
    delay(500); //don't turn on all the LEDs if the button is kept on pressing
  } 
  if (ETButton) { 
    // set the time when the LED is turned on
    StartTime = millis();
    for (int i=0; i<= ETcounter; i++) {
      CircuitPlayground.setPixelColor(i, Color1);  
    }
    delay(100);
    ETcounter++;
    if ((ETcounter < 0) || (ETcounter > Upperlimit)) {
      CircuitPlayground.clearPixels();
      if (ETcounter > Upperlimit) {
        happyFace();
        MusicMode = !MusicMode;     
      }
      ETcounter = 0; // for now we set it back to 0 but should hcange this
    }
   } else {
    checkTimer();
   }  
}

void checkTimer() {
  unsigned long ElapsedTime;
  unsigned long CurrentTime = millis();
  
  ElapsedTime = CurrentTime - StartTime;
  
  if ((ElapsedTime < 2*ETseconds) && (ElapsedTime > ETseconds) ) {
    CircuitPlayground.setPixelColor(ETcounter-1, Color2); 
  } else if ((ElapsedTime > 2*ETseconds) && (ElapsedTime < 3*ETseconds)) {
    CircuitPlayground.setPixelColor(ETcounter-1, Color3); 
  } else if (ElapsedTime > 3*ETseconds) {
    CircuitPlayground.setPixelColor(ETcounter-1, Color4); // this LED is turned off
    StartTime = millis();  // restart the timer 
    ETcounter--;           // and go back one LED
  }
}

void happyFace() {
  CircuitPlayground.clearPixels();
  delay(500);
  int happyFace[6] = {0, 1, 4, 5, 8, 9};
  if (!MusicMode) {
    for (int h = 0; h < 6 ; h++) {
      CircuitPlayground.setPixelColor(happyFace[h], White); 
    }
    playHappyMusic();   
  } else {
    for (int h = 0; h < 6 ; h++) {
      CircuitPlayground.setPixelColor(happyFace[h], Color1); 
    }
    playDartVaderMusic(); 
    
    
  }
  delay(2000);
  CircuitPlayground.clearPixels();
  //ETcounter = 0;
}

void playDartVaderMusic () {
  // iterate over the notes of the melody. 
  // array is twice the number of notes (notes + durations)
  
  for (int thisNote = 0; thisNote < notes * 2; thisNote = thisNote + 2) {

    // calculates the duration of mieach note
    divider = melody[thisNote + 1];
    if (divider > 0) {
      // regular note, just divide
      noteDuration = (wholenote) / divider;
    } else if (divider < 0) {
      // dotted notes are represented with negative durations
      noteDuration = (wholenote) / abs(divider);
      noteDuration *= 1.5; // increases the duration in half for dotted notes
    }

    // play the note for 90% of the duration, leaving 10% as a pause
//   if connected to arduino use: tone(buzzer, melody[thisNote], noteDuration*0.9);
    CircuitPlayground.playTone(melody[thisNote], noteDuration*0.5);
    // Wait for the  duration before playing the next note/shortened the time
    delay(noteDuration*0.3);
    
  }
}

void playHappyMusic() {
     
  for (int thisNote1 = 0; thisNote1 < notes1 * 2; thisNote1 = thisNote1 + 2) {

    // calculates the duration of each note
    divider = melody1[thisNote1 + 1];
    if (divider > 0) {
      // regular note, just divide
      noteDuration = (wholenote) / divider;
    } else if (divider < 0) {
      // dotted notes are represented with negative durations
      noteDuration = (wholenote) / abs(divider);
      noteDuration *= 1.5; // increases the duration in half for dotted notes
    }

    // play the note for 90% of the duration, leaving 10% as a pause
//   if connected to arduino use: tone(buzzer, melody[thisNote], noteDuration*0.9);
    CircuitPlayground.playTone(melody1[thisNote1], noteDuration*0.3);
    // Wait for the  duration before playing the next note/shortened the time
    delay(noteDuration*0.2);
    
  }
  
 }
