# Smart Lighting Control Blueprint - User Guide

## **Overview**

This blueprint provides advanced room lighting control based on occupancy, illuminance, and sleep mode. It dynamically adjusts lighting conditions based on multiple user-defined inputs, offering both manual configuration and sensor-based automation.

---

## **How to Use This Blueprint**

### **Inputs**

The blueprint includes several inputs that allow you to customize how your smart lighting behaves. Below is a detailed explanation of each input field:

---

### **1. Area Lights**

- **Description**: The lights to control in your defined area.
- **Type**: Target (select one or more entities).
- **How to Use**:
  - Choose the lights you want to automate.
  - You can select one or multiple lights from the available entities in your Home Assistant setup.

---

### **2. Occupancy Sensor**

- **Description**: A binary sensor that detects whether the area is occupied.
- **Type**: Entity (binary_sensor, occupancy device class).
- **How to Use**:
  - Select an occupancy sensor (e.g., a motion sensor) that detects presence in the room.

---

### **3. Illuminance Sensor**

- **Description**: A sensor that measures the brightness level (lux) in the room.
- **Type**: Entity (sensor, illuminance device class).
- **How to Use**:
  - Select an illuminance sensor that will determine the current brightness level in the room.

---

### **4. Illuminance Threshold**

#### **a. Illuminance Threshold Sensor**

- **Description**: A sensor or input number entity that provides a threshold value for brightness (in lux).
- **Type**: Entity (sensor, input_number, illuminance device class).
- **How to Use**:
  - Choose an entity that holds a dynamic threshold value for room brightness. This allows the blueprint to adjust based on real-time data.

#### **b. Illuminance Threshold (Optional)**

- **Description**: A fixed brightness threshold (in lux) below which the lights should turn on.
- **Type**: Number (manual entry).
- **Default**: 10 lux.
- **How to Use**:
  - If you don’t have a sensor for the threshold, specify a numeric value. This value will act as the fallback when no sensor is selected.

---

### **5. Sleep Mode**

#### **a. Sleep Mode Sensor**

- **Description**: A binary sensor or input boolean that indicates whether the system is in sleep mode.
- **Type**: Entity (input_boolean, binary_sensor).
- **How to Use**:
  - Select an entity that triggers sleep mode (e.g., an "Away" toggle or a night mode sensor).

---

### **6. People Home**

- **Description**: A binary sensor that detects if anyone is home.
- **Type**: Entity (binary_sensor).
- **How to Use**:
  - Select a binary sensor that indicates occupancy of the house (e.g., a person tracker or geofence sensor).

---

### **7. Brightness Settings**

#### **a. Maximum Brightness Sensor**

- **Description**: A sensor or input number entity that defines the maximum brightness level (%).
- **Type**: Entity (sensor, input_number).
- **How to Use**:
  - Choose an entity that provides a dynamic maximum brightness value.

#### **b. Maximum Brightness (Optional)**

- **Description**: A fixed brightness level for normal mode.
- **Type**: Number (manual entry).
- **Default**: 100%.
- **How to Use**:
  - Specify a value if you don’t use a sensor for maximum brightness.

#### **c. Minimum Brightness Sensor**

- **Description**: A sensor or input number entity that defines the minimum brightness level during sleep mode (%).
- **Type**: Entity (sensor, input_number).
- **How to Use**:
  - Choose an entity that provides a dynamic minimum brightness value.

#### **d. Minimum Brightness (Optional)**

- **Description**: A fixed brightness level during sleep mode.
- **Type**: Number (manual entry).
- **Default**: 10%.
- **How to Use**:
  - Specify a value if you don’t use a sensor for minimum brightness.

---

### **8. Transition Time**

#### **a. Transition Time Sensor**

- **Description**: A sensor or input number entity that specifies how long it takes for lights to transition between states (in seconds).
- **Type**: Entity (sensor, input_number).
- **How to Use**:
  - Select a dynamic source for the transition time if required.

#### **b. Transition Time (Optional)**

- **Description**: A fixed transition duration (in seconds).
- **Type**: Number (manual entry).
- **Default**: 2 seconds.
- **How to Use**:
  - Specify the transition time if you don’t use a sensor.

---

### **9. Idle Timeout**

#### **a. Idle Timeout Sensor**

- **Description**: A sensor or input number entity that specifies how long the lights stay on after the room becomes unoccupied (in seconds).
- **Type**: Entity (sensor, input_number).
- **How to Use**:
  - Select an entity that dynamically determines the timeout duration.

#### **b. Idle Timeout (Optional)**

- **Description**: A fixed timeout duration (in seconds).
- **Type**: Number (manual entry).
- **Default**: 300 seconds.
- **How to Use**:
  - Specify the timeout duration if you don’t use a sensor.

---

## **Triggers**

The automation reacts to the following events:

1. Changes in the **occupancy sensor**.
2. Updates in the **illuminance sensor** or **illuminance threshold sensor**.
3. State changes in **sleep mode** or **people home**.
4. Home Assistant start-up events.

---

## **Conditions**

The automation ensures:

- Lights only activate when the **People Home** sensor indicates someone is home.
- Lights adjust according to the configured thresholds, sleep mode, and brightness settings.

---

## **Actions**

The blueprint intelligently adjusts the lights:

- **When occupied**:
  - Turns on the lights with brightness based on **max/min brightness** and **sleep mode**.
- **When unoccupied**:
  - Turns off the lights after the specified idle timeout.
  - Optionally dims the lights before turning them off.

---

## **Example Configuration**

For a living room:

1. **Area Lights**: `light.living_room_ceiling`, `light.living_room_lamp`.
2. **Occupancy Sensor**: `binary_sensor.motion_living_room`.
3. **Illuminance Sensor**: `sensor.living_room_lux`.
4. **Illuminance Threshold Sensor**: `input_number.living_room_threshold`.
5. **Illuminance Threshold**: Leave blank (use the sensor value).
6. **Sleep Mode Sensor**: `input_boolean.night_mode`.
7. **Maximum Brightness**: 80%.
8. **Minimum Brightness**: 20%.
9. **Transition Time**: 5 seconds.
10. **Idle Timeout**: 600 seconds.

This configuration ensures a fully automated lighting system tailored to your preferences.
