# OpenFrame Overview

The OpenFrame Project provides an empty harness chip that differs significantly from the Caravel and Caravan designs. Unlike Caravel and Caravan, which include integrated SoCs and additional features, OpenFrame offers only the essential padframe, providing users with a clean slate for their custom designs.

<img width="256" alt="Screenshot 2024-06-24 at 12 53 39 PM" src="https://github.com/efabless/openframe_timer_example/assets/67271180/ff58b58b-b9c8-4d5e-b9bc-bf344355fa80">

## Key Characteristics of OpenFrame

1. **Minimalist Design:** 
   - No integrated SoC or additional circuitry.
   - Only includes the padframe, a power-on-reset circuit, and a digital ROM containing the 32-bit project ID.

2. **Padframe Compatibility:**
   - The padframe design and pin placements match those of the Caravel and Caravan chips, ensuring compatibility and ease of transition between designs.
   - Pin types are identical, with power and ground pins positioned similarly and the same power domains available.

3. **Flexibility:**
   - Provides full access to all GPIO controls.
   - Maximizes the user project area, allowing for greater customization and integration of alternative SoCs or user-specific projects at the same hierarchy level.

4. **Simplified I/O:**
   - Pins that previously connected to CPU functions (e.g., flash controller interface, SPI interface, UART) are now repurposed as general-purpose I/O, offering flexibility for various applications.

The OpenFrame harness is ideal for those looking to implement custom SoCs or integrate user projects without the constraints of an existing SoC.

## Features

1. 44 configurable GPIOs.
2. User area of approximately 15mm².
3. Supports digital, analog, or mixed-signal designs.


# Microwatt Smart Peripherals SoC

## Project Proposal and Description

This project presents a **minimal System-on-Chip (SoC) based on the open-source Microwatt CPU core**, enhanced with smart peripherals including **UART, GPIO, and SPI/I²C**. The design demonstrates real-world embedded applications such as:

- Controlling LEDs via GPIO  
- Reading data from a temperature sensor via I²C  
- Communicating system status over UART  

The objective is to showcase that **Microwatt can serve as the central processor of a microcontroller-like system**, providing a fully functional, reproducible, and educational platform for open-source hardware development.

---

## Significance and Impact

- **Complete SoC Implementation:** Integrates CPU and peripheral subsystems to deliver a fully operational design.  
- **Reproducibility and Accessibility:** Facilitates replication and experimentation by judges and the community.  
- **Educational Value:** Serves as a reference platform for developers and learners exploring Microwatt and embedded SoC design.

---

## Distinguishing Features

- **Smart Peripheral Extensions:**  
  - PWM output for LED dimming or motor control  
  - ADC interface to connect analog sensors  

- **Configurable Memory-Mapped Bus:**  
  - Implemented using **Wishbone or AXI-lite interconnect** for modularity  
  - Enhances reusability and scalability of the design  

- **Demonstration Application – “Microwatt Smart Node”:**  
  - Reads sensor data via I²C  
  - Transmits sensor information over UART  
  - Dynamically adjusts LED blink rate based on temperature readings  

- **Optional Debug Module:**  
  - Provides JTAG/UART-based memory and register access  
  - Enables debugging and instructional demonstrations  

> This SoC extends beyond a simple Microwatt implementation, representing a **smart edge computing device** with complete hardware-software integration suitable for prototyping, education, and open-source innovation.

---

## Expected Deliverables

- RTL code for Microwatt core with integrated peripherals  
- Conceptual block diagram illustrating CPU → Peripherals → Demonstration Applications  
- Plan for demonstrating embedded applications including LED control, sensor readings, and UART communication  

---



## OpenFrame Overview

The OpenFrame Project provides an empty harness chip that differs significantly from the Caravel and Caravan designs. Unlike Caravel and Caravan, which include integrated SoCs and additional features, OpenFrame offers only the essential padframe, providing users with a clean slate for their custom designs.

## Installation and Setup

First, clone the repository:

```bash
git clone https://github.com/efabless/openframe_timer_example.git
cd openframe_timer_example
```

Then, download all dependencies:

```bash
make setup
```

## Hardening the Design

In this example, we will harden the timer. You will need to harden your own design similarly.

```bash
make user_proj_timer
```

Once you have hardened your design, integrate it into the OpenFrame wrapper:

```bash
make openframe_project_wrapper
```

## Important Notes

1. **Connecting to Power:**
   - Ensure your design is connected to power using the power pins on the wrapper.
   - Use the `vccd1_connection` and `vssd1_connection` macros, which contain the necessary vias and nets for power connections.

2. **Flattening the Design:**
   - If you plan to flatten your design within the `openframe_project_wrapper`, do not buffer the analog pins using standard cells.

3. **Running Custom Steps:**
   - Execute the custom step in OpenLane that copies the power pins from the template DEF. If this step is skipped, the precheck will fail, and your design will not be powered.
