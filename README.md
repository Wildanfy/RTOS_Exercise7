# RTOS-EXERCISE 7
![image](https://github.com/user-attachments/assets/d77d6e0b-e041-4543-b500-a8efe4950d13)


# STM32 FreeRTOS LED Control Project

## Description
This project demonstrates a multi-threaded application running on an STM32 microcontroller using FreeRTOS. The application controls multiple LEDs connected to GPIO pins, with each LED being managed by a dedicated FreeRTOS task. The tasks demonstrate critical section handling to access shared resources safely.

## Features
- **FreeRTOS Integration:** The project leverages FreeRTOS for multi-threaded operations.
- **Multi-LED Control:** Each LED is controlled by a separate task with independent blink rates.
- **Critical Section Handling:** Proper handling of shared resources using FreeRTOS critical section APIs.
- **Simulated Shared Resource Access:** Includes a simulated read-write operation on shared data.

## Project Structure
The key components of this project include:
- **Tasks:**
  - `GreenLedTask`: Controls the green LED (GPIOA Pin 0) with a 200ms delay.
  - `RedLedTask`: Controls the red LED (GPIOA Pin 1) with a 550ms delay.
  - `OrangeLedTask`: Toggles the orange LED (GPIOA Pin 3) every 50ms.
- **Shared Resource:** A `startFlag` variable, used to simulate shared data access.
- **Simulated Delay Function:** Implements a loop-based delay to mimic processing.

## Hardware Requirements
1. **STM32 Microcontroller**: Compatible with STM32CubeIDE (tested on STM32F401VGT6).
2. **LEDs**: At least three LEDs connected to GPIOA pins (Pin 0, Pin 1, Pin 3).
3. **Power Supply**: Provide adequate power for the STM32 board and peripherals.

## Software Requirements
1. **STM32CubeIDE**: Used for development and debugging.
2. **FreeRTOS**: Integrated as part of the STM32Cube HAL library.
3. **CMSIS-RTOS API**: For FreeRTOS task and kernel management.

## How It Works
1. **Initialization**:
   - HAL library initializes peripherals.
   - FreeRTOS kernel starts, and tasks are created.

2. **Task Functions**:
   - Each task toggles or sets its associated LED based on a fixed delay.
   - Tasks enter critical sections when accessing shared data (`startFlag`).

3. **Critical Section**:
   - The `taskENTER_CRITICAL()` and `taskEXIT_CRITICAL()` macros ensure safe access to `startFlag` during LED control.

## Configuration
### GPIO
- Configure GPIO pins for LEDs:
  - Green LED: GPIOA Pin 0
  - Red LED: GPIOA Pin 1
  - Orange LED: GPIOA Pin 3

### FreeRTOS Tasks
- Modify task definitions in `main.c` if additional LEDs or functionalities are required.

## Code Snippets
### Task Creation
```c
osThreadDef(HijauLedTask, GreenLedTask, osPriorityNormal, 0, 128);
HijauLedTaskHandle = osThreadCreate(osThread(HijauLedTask), NULL);
```

### Critical Section Example
```c
taskENTER_CRITICAL();
accessSharedData();
taskEXIT_CRITICAL();
```

### Simulated Shared Data Access
```c
void accessSharedData(void) {
    if (startFlag == 1) {
        startFlag = 0;
    } else {
        HAL_GPIO_WritePin(GPIOA, GPIO_PIN_2, GPIO_PIN_SET);
    }
    SimulateReadWriteOperation();
    startFlag = 1;
    HAL_GPIO_WritePin(GPIOA, GPIO_PIN_2, GPIO_PIN_RESET);
}
```

## Usage
1. Clone this repository to your local machine.
2. Open the project in STM32CubeIDE.
3. Compile and flash the code onto your STM32 microcontroller.
4. Observe the LEDs blinking based on the specified task logic.


## IOC Pin
![image](https://github.com/user-attachments/assets/3f940ffa-fa43-4598-9acd-4c7dff07e2ec)



## Demo Video
https://github.com/user-attachments/assets/797069b3-24ff-4e49-a5a0-b19c0b02cdf5
## Contributor
- Wildan Faizin (3222600011)
- Dhanang Fadhila Trisnandi (3222600015)
