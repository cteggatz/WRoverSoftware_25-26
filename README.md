# WRoverSoftware_25-26
Official Wisconsin Robotics software repository for the 2026 University Rover Challenge, containing autonomy, control, and base station code. For information about the code & project architecture itself, please refer to docs folder. 
- [Battery Estimator Documentation](./docs/Battery_Telemetry.md)

# Telemetry Build & Start
Here are the instructions for building and starting any telemetry project.

### Hardware - ROS2 bridge

### Battery Telemetry Estimator Firmware
for building firmware you need to the respective [firmware folder](./src/firmware/) and flash it onto the microcontroller. To flash it onto the STM32 board you need to make use of a ST-Link STM32 programmer and [STM's CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html).

1. Open the project in CubeIDE
2. plug your microcontroller into your PC with the ST-Link programmer
3. Build with the green arrow button in CubeIDE.

