# 🚦 Arduino Traffic Light System with Pedestrian Button

A simple and interactive **traffic signal system** built using **Arduino UNO**, LEDs, resistors, and a push button.
When no one presses the button, the **green light stays ON**.
When the pedestrian button is pressed, the system switches to **yellow → red**, giving safe crossing time.

I have also added a video demo in this repository to show the working project.

## Features

* 🟢 **Green light ON by default**
* 🟡 **Yellow warning light when the pedestrian button is pressed**
* 🔴 **Red light for pedestrian crossing**
* ⏱️ Includes real timing delays (5s for waiting, 10s for crossing)
* 🖥️ Serial Monitor logs the status in real time
* 🔌 Works on an Arduino UNO with simple components (no complex hardware)

---

## Components Used

* Arduino Uno
* 3 LEDs (Red, Yellow, Green)
* Push Button
* 220Ω resistors
* Breadboard + Jumper wires
* USB cable for power/programming

## 🔌 Circuit Diagram

The LEDs are connected to digital pins:

| LED    | Arduino Pin |
| ------ | ----------- |
| Green  | 12          |
| Yellow | 11          |
| Red    | 10          |

The push button is connected to **pin 7** (with ground reference).

I’ve added the full circuit diagram image in this repo.

## 💻 Code

```cpp
int red=10;
int yellow=11;
int green=12;

int pushButton=7;
int readPushbutton=0;

void setup()
{
  pinMode(red,OUTPUT);
  pinMode(yellow,OUTPUT);
  pinMode(green,OUTPUT);
  pinMode(pushButton,INPUT);
  
  digitalWrite(red,LOW);
  digitalWrite(yellow,LOW);
  digitalWrite(green,LOW);
  
  Serial.begin(9600);
}

void loop()
{
  int readPushbutton=digitalRead(pushButton);
  
  // Default condition (no pedestrian)
  if(readPushbutton==0)
  {
    digitalWrite(green,HIGH);
    digitalWrite(yellow,LOW);
    digitalWrite(red,LOW);
  }
  
  // Pedestrian button pressed
  else if(readPushbutton==1)
  {
    digitalWrite(green,LOW);
    digitalWrite(yellow,HIGH);
    digitalWrite(red,LOW);
    Serial.print("Pedestrian is waiting...\n");
    delay(5000);
    
    digitalWrite(green,LOW);
    digitalWrite(yellow,LOW);
    digitalWrite(red,HIGH);
    Serial.print("Pedestrian crossing...\n");
    delay(10000);
  }
}
```

---

## 🎬 Demo Video

I have included a **demo video** in this repository showing the real hardware working.


## 📚 How It Works

1. **Normal mode:** Green LED stays ON
2. **Button pressed:**

   * Yellow light turns ON → indicates transition
   * After delay, Red light turns ON → pedestrians cross
3. After crossing time, the system returns to **green**

This simulates a basic real-world pedestrian traffic signal system.

