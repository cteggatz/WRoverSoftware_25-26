# Battery Telemetry
this document outlines the software side of the battery telemetry project. For electrical engineering documentation, refer to the Wisconsin Robotics Google Drive.

## General Overview
### Diagram
``` Mermaid
flowchart LR
    subgraph PCB [Battery Estimation PCB]
        direction LR
        Hardware_Timer -->|500ms| A
        A[ADC] --> ADC_ReadyInterupt
        subgraph STM [STM32F103C8T6]
            ADC_ReadyInterupt --> RTOS_ReadADC
            RTOS_ReadADC -.-|Semiphore or double buffer| L[RTOS_Serial_Write & RTOS_Serial_Read]

        end
    end
    subgraph Jetson [NVIDIA Jetson]
        L <==>|UART serial communcation USB or JetsonPinout| C[ROS Battery Server]
    end
    subgraph base [Base Station]
        C <==> |ROS2 Topic| D[GUI]
    end
```

### Design Choices
#### ROS Battery Server
A ROS2 Server was chosen as the architecture for the communication with the Microcontroller because there is not a need for continous communication. At most the GUI will query or publish a command to the server every now and then.

The Server needs to acomplish a couple of tasks:
1. Facilitate communcations between the board and ROS
2. be able to process and send packets to the Base Station

#### UART Communaction
UART communcation was chosen vs MicroROS simply because of size contraints. The STM32 STM32F103C8T6 Bluepill model being used simply doesn't have enough flash memory to facilitate MicroROS on the board, especially with FreeRTOS already running on the board

#### STM32
On the STM32 board itself it will facilitate multiple tasks, but for the purposes of battery telemetry it will do the coulomb counting calculations and communicate with the server.



