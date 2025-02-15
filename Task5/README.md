# Traffic Light Controller Using Ultrasonic Sensors in RISC-V Processor

## **Overview**  
A RISC-V-based traffic light controller utilizes **ultrasonic sensors** to detect vehicle presence and density, dynamically adjusting signal timing to optimize traffic flow, reduce congestion, enhance safety, and improve overall intersection efficiency.  

## **Components Required**  
- **RISC-V Processor**  
- **Ultrasonic Sensors**  
- **Traffic Light System (LEDs or Relays)**  
- **Power Supply**  
- **Resistors and Jumper Wires**  

## **Circuit Connection**  
The **ultrasonic sensors** are connected to the **RISC-V Processor** as follows:  
- **VCC (Power) → P5V pin** on the processor board  
- **GND (Ground) → P_GND pin** on the board  
- **Trigger Pin → P10 (Sends ultrasonic pulse)**  
- **Echo Pin → P11 (Receives reflected signal)**  

The **traffic light system** is controlled by the **RISC-V Processor** through GPIO pins:  
- **Red Light → P2**  
- **Yellow Light → P3**  
- **Green Light → P4**  
- **Buzzer → P6**  
- **Laser Sensor → P12**  

## 📌 **Pin Connections**  
### **1️⃣ Ultrasonic Sensor**  
| **Sensor Pin** | **RISC-V Pin** | **Description** |  
|---------------|----------------|----------------|  
| **VCC**       | **P5V**        | Power Supply  |  
| **GND**       | **P_GND**      | Ground        |  
| **TRIG**      | **P10**        | Trigger Signal (Output) |  
| **ECHO**      | **P11**        | Echo Response (Input) |  

### **2️⃣ Traffic Light System**  
| **Traffic Light** | **RISC-V Pin** | **Description** |  
|------------------|----------------|----------------|  
| **Red Light**     | **P2**         | Stop Signal |  
| **Yellow Light**  | **P3**         | Prepare to Stop |  
| **Green Light**   | **P4**         | Go Signal |  
| **Buzzer**        | **P6**         | Alert Sound |  
| **Laser Sensor**  | **P12**        | Obstruction Detection |  

## 📌 **Working Process**  
### *Step-by-Step Working of the Traffic Light System with Buzzer & Laser Sensor*  
This system simulates a *traffic light sequence* and uses a *laser sensor* to detect obstructions. If an obstruction is detected, a *buzzer* will alert the user.  

### *1️⃣ System Initialization*  
- The *RISC-V Processor* initializes and configures the *GPIO pins*.  
- *LEDs (Red, Yellow, Green) & Buzzer* are set as *output*.  
- *Laser Sensor* is set as *input* (P12).  

### *2️⃣ Main Working Loop*  
The system runs in a continuous loop, executing the *traffic light sequence*:  

#### *🔴 Step 1: Red Light ON (Stop)*  
- *Red LED (P2) turns ON*.  
- *Yellow & Green LEDs remain OFF*.  
- *Laser Sensor checks for obstruction*:  
  - If *no obstruction (Laser Sensor = 1)* → Buzzer OFF.  
  - If *obstruction detected (Laser Sensor = 0)* → Buzzer ON.  
- *Delay:* 5 seconds.  

#### *🟠 Step 2: Red + Yellow Light ON (Prepare to Go)*  
- *Red LED (P2) & Yellow LED (P3) turn ON*.  
- *Green LED remains OFF*.  
- *Laser Sensor checks for obstruction*:  
  - If *no obstruction* → Buzzer OFF.  
  - If *obstruction detected* → Buzzer ON.  
- *Delay:* 2 seconds.  

#### *🟢 Step 3: Green Light ON (Go)*  
- *Green LED (P4) turns ON*.  
- *Red & Yellow LEDs turn OFF*.  
- *Buzzer turns OFF regardless of the laser sensor*.  
- *Delay:* 5 seconds.  

#### *🟠 Step 4: Yellow Light ON (Slow Down)*  
- *Only Yellow LED (P3) turns ON*.  
- *Red & Green LEDs remain OFF*.  
- *Laser Sensor checks for obstruction*:  
  - If *no obstruction* → Buzzer OFF.  
  - If *obstruction detected* → Buzzer ON.  
- *Delay:* 2 seconds.  

### *3️⃣ Repeat Cycle*  
- The sequence *repeats indefinitely* every *14 seconds*.  
- *If an obstruction is detected* at any step *except when Green is ON, the **buzzer will sound an alert***.  

### *Final Behavior Summary*  
- *Normal Traffic Flow:* Follows *Red → Red+Yellow → Green → Yellow → Red*.  
- *Buzzer Alerts:* Sounds *only during Red, Red+Yellow, and Yellow* if an obstruction is detected.  
- *Green Light Priority:* The *buzzer is always OFF when the Green LED is ON.*  

## 📌 **Truth Table**  
| **S1** | **S0** | **L (Laser Sensor)** | **R (Red LED)** | **Y (Yellow LED)** | **G (Green LED)** | **B (Buzzer)** | **State Description** |  
|------|------|----------------|-------------|--------------|-------------|------------|------------------|  
| 0    | 0    | 1              | 1           | 0            | 0           | 0          | Red Light ON (No obstruction) |  
| 0    | 0    | 0              | 1           | 0            | 0           | 1          | Red Light ON (Obstruction detected - Buzzer ON) |  
| 0    | 1    | 1              | 1           | 1            | 0           | 0          | Red & Yellow Light ON (No obstruction) |  
| 0    | 1    | 0              | 1           | 1            | 0           | 1          | Red & Yellow Light ON (Obstruction detected - Buzzer ON) |  
| 1    | 0    | X              | 0           | 0            | 1           | 0          | Green Light ON (Buzzer OFF, Laser sensor ignored) |  
| 1    | 1    | 1              | 0           | 1            | 0           | 0          | Yellow Light ON (No obstruction) |  
| 1    | 1    | 0              | 0           | 1            | 0           | 1          | Yellow Light ON (Obstruction detected - Buzzer ON) |  
