# Ultrasonic Obstacle Detection using VSDSquadron Mini

## Overview
This project implements an **ultrasonic obstacle detection system** using an **HC-SR04 ultrasonic sensor** and an **active buzzer** on the **VSDSquadron Mini Board**. The system detects obstacles and provides **audible alerts** based on distance.

---
## Code Implementation

```c
#include <ch32v00x.h>

// Define GPIO pins
#define RED_LED GPIO_Pin_3  // PC3 (A < B)
#define GREEN_LED GPIO_Pin_4  // PC4 (A == B)
#define YELLOW_LED GPIO_Pin_5  // PC5 (A > B)
#define BUZZER GPIO_Pin_6  // Example: PC6
#define LASER_SENSOR GPIO_Pin_0  // PD0 (Example sensor input)

void GPIO_Config(void) {
    GPIO_InitTypeDef GPIO_InitStructure;

    // Enable GPIO clocks for port C and D
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC, ENABLE);
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE);

    // Configure LED and buzzer as output
    GPIO_InitStructure.GPIO_Pin = RED_LED | GREEN_LED | YELLOW_LED | BUZZER;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOC, &GPIO_InitStructure);

    // Configure laser sensor as input
    GPIO_InitStructure.GPIO_Pin = LASER_SENSOR;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;  // Pull-up input
    GPIO_Init(GPIOD, &GPIO_InitStructure);
}
```
---

## 2. Expected Output
| Scenario               | Distance (cm) | Buzzer Output             |
|------------------------|--------------|---------------------------|
| **No Object Detected** | 0            | OFF                       |
| **Very Close Object**  | <10          | Continuous Beep (ON)      |
| **Medium Distance**    | 10 - 30      | Beeps (500ms ON/OFF)      |
| **Far Object**         | >30          | OFF                       |
| **Object Removed**     | No reading   | OFF                       |

---

## 3. Future Enhancements
This project can be enhanced with:
- **Multiple Distance Zones:** Add more buzzer patterns for different distances.
- **Voice Alerts:** Use a **Text-to-Speech (TTS)** module for spoken alerts.
- **Bluetooth/Wi-Fi Integration:** Connect the system to a mobile app for remote monitoring.
- **Battery Optimization:** Reduce power consumption for longer operation.

---

## 4. Conclusion
This **ultrasonic obstacle detection system** provides a cost-effective, real-time solution for **visually impaired users** and other object detection applications. It is a **simple yet effective implementation** that can be further improved with additional features.
