# 🔧 RISC-V Based SoC Design: SPI Protocol Interface

![Project Banner](https://img.shields.io/badge/RTL--to--SoC-Verified-blue?style=for-the-badge) 

A complete System-on-Chip (SoC) design integrating a Verilog-based SPI controller with a RISC-V ET1035 processor, tested through both simulation and hardware implementation on the ARTY A7 FPGA. The system includes a real-world temperature monitoring application interfaced via Arduino and DHT11 sensor.

---

## 📌 Project Overview
This project demonstrates the implementation of a full-duplex SPI controller in Verilog, integration with a RISC-V processor core, and deployment on an FPGA board. The design supports:

- Configurable SPI protocol (CPOL, CPHA, baud rate)
- Interrupt support for transmit/receive
- Modular register architecture (Control, Status, Data)
- Real-time data handling from temperature sensors

---

## 🧩 System Architecture
```
[ Arduino (Sensor Input) ]
       ↓ UART
[ RISC-V ET1035 CPU ]
       ↓
[ SPI Controller ] ⇄ [ SPI Slave ]
       ↓                 ↑
    (GPIO/LED)     (MOSI/MISO/SCLK)
       ↓                 ↑
 
```

---

## 🔧 Implementation Details
### Firmware:
- `main.c`, `SPI.c`, `SPI.h`, and `config.h`
- Mapped memory using base address `0x30000600`

### Hardware:
- Verilog RTL for SPI Master and SoC integration
- Finite State Machine controlling TX/RX
- Baud rate control, CPHA/CPOL logic
- Synthesis and bitstream generation using Vivado

---

## 🛠️ Registers Used
- **SPICR1/2**: Control registers for mode, interrupt, polarity
- **SPISR**: Status (SPIF, MODF, TXE, RXE)
- **SPIDR**: Data register
- **Baud Rate**: SPI frequency selection

---

## 🧪 Testing & Results
### ✅ Simulation:
- RTL verified using Vivado with testbenches for TX and RX
- Functional verification of SPICR settings

### ✅ Hardware:
- Artix-7 FPGA (ARTY A7)
- Sensor data sent via Arduino → UART → RISC-V → SPI Controller
- Real-time LED alert and UART monitor output

| Scenario | Output |
|---------|--------|
| Temp < 30°C | LED OFF + UART displays value |
| Temp > 30°C | LED ON + UART alerts high temp |

---

## 📈 Project Highlights
- 🌐 Real-time sensor interfacing on FPGA
- 🛠️ Modular register design
- 🔄 Parallel-to-Serial data conversion logic
- 💡 Fully parameterized Verilog modules
- ✅ Verified through simulation and real hardware

---

## 📚 Future Scope
- Multi-slave SPI arbitration
- DMA integration for zero-latency data transfer
- Extend to I2C/UART for hybrid communication SoC
- Add error-checking and CRC support

---

> Designed as part of Minor Project @ KLE Technological University under the guidance of **Dr. Saroja Siddamal**

---

## 📎 Resources
- [SPI Protocol Wikipedia](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface)
- [Vivado FPGA Tool](https://www.xilinx.com/products/design-tools/vivado.html)

---

**Made with 💻 for Embedded SoC Innovation.**
