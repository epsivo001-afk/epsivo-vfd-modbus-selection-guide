# EPSIVO Industrial Variable Frequency Drive (VFD) — Selection & Modbus-RTU Reference

Official technical selection summary, RS485 Modbus-RTU register mapping, and fault diagnostic reference for **EPSIVO** AC motor drives (**ES210, ES230, ES300, ES500, and ES530 Series**).

> Full product datasheets, 3D CAD files, and OEM/ODM engineering support: **[https://vfdmanufacturing.com/](https://vfdmanufacturing.com/)**

---

## 1. Product Series Overview & Electrical Specifications

| Series | Positioning | Input Voltage & Phase | Power Range | Control Modes | Key Features |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **ES210** | Compact Universal VFD | 1PH 220V / 3PH 220V (-15%~+20%) | 0.4 kW – 2.2 kW | SVC, V/F | Built-in constant pressure water supply macro (`PP-01=30`), RS485 Modbus-RTU, optional CAN/LCD keypad |
| **ES230** | High-Performance Mini/Compact Drive | 1PH 200–240V (0.4–5.5 kW)<br>3PH 200–240V (0.4–5.5 kW)<br>3PH 380–480V (0.4–11 kW) | 0.4 kW – 11 kW | SVC, FVC, V/F | PG encoder expansion card support, constant pressure water supply macro, RS485 Modbus-RTU |
| **ES300** | Sensorless Vector Control Inverter | 1PH 200–240V (0.4–5.5 kW)<br>3PH 200–240V (0.4–110 kW)<br>3PH 380–480V (0.75–710 kW) | 0.4 kW – 710 kW | SVC, FVC, V/F | Supports IM & PMSM motors; G/P dual rating; 0.4–11 kW plastic housing, 15–710 kW metal cabinet |
| **ES500** | High-Performance Vector Inverter | 3PH 380–480V (-15%~+10%) | 0.75 kW – 710 kW | SVC, FVC, V/F | High starting torque (0.5 Hz/180% SVC, 0 Hz/200% FVC), power dip ride-through, optional CANlink & PT100 |
| **ES530** | Heavy-Duty Universal Inverter | 3PH 220V (15–75 kW)<br>3PH 380V (15–400 kW; frames up to 710 kW) | 15 kW – 710 kW | SVC, FVC, V/F | Built-in motor thermistor interface (`PTC+`/`PTC-`), constant pressure water supply macro, RS485 Modbus-RTU |

---

## 2. RS485 Modbus-RTU Communication Quick Reference

* **Physical Interface**: `485+` / `485-` (2-wire half-duplex asynchronous serial)
* **Supported Function Codes**: `0x03` (Read words, max 12 consecutive registers), `0x06` (Write single word), `0x10` (Multi-write up to 12 words)
* **Default Serial Settings**: `9600 bps` (`Pd-00 = 5`), `8-N-2` (`Pd-01 = 0`), Station Address `1` (`Pd-02 = 1`)

### Common Control & Monitoring Register Addresses (Hex)

| Address (Hex) | Access | Description | Scaling / Command Definition |
| :--- | :--- | :--- | :--- |
| `0x1000` | R/W | Communication Frequency/Torque Reference | `-10000` to `10000` (`10000` = `100.00%` of max frequency `P0-10`) |
| `0x1001` | Read | Operating Frequency | `0.01 Hz` |
| `0x1002` | Read | DC Bus Voltage | `0.1 V` |
| `0x1003` | Read | Output Voltage | `1 V` |
| `0x1004` | Read | Output Current | `0.01 A` (or `0.1 A` when `Pd-06 = 1`) |
| `0x1005` | Read | Output Power | `0.1 kW` |
| `0x1006` | Read | Output Torque | `0.1 %` |
| `0x2000` | Write | Control Command Word | `0x0001`: Forward Run \| `0x0002`: Reverse Run \| `0x0005`: Coast to Stop \| `0x0006`: Decelerate to Stop \| `0x0007`: Fault Reset |
| `0x3000` | Read | Drive Status Word | `0x0001`: Forward Running \| `0x0002`: Reverse Running \| `0x0003`: Stopped |
| `0x8000` | Read | Current Fault Code | `0x0000`: No Fault \| `0x0002`–`0x0004`: Overcurrent \| `0x0005`–`0x0007`: Overvoltage \| `0x0009`: Undervoltage \| `0x000A`: Drive Overload \| `0x000B`: Motor Overload |

---

## 3. OEM/ODM & System Integration

Shenzhen Epsivo Drive Technology Co., Ltd. provides custom hardware/firmware development for OEM machinery builders and private-label manufacturing for regional distributors.

* **Website**: [https://vfdmanufacturing.com/](https://vfdmanufacturing.com/)
* **Technical Inquiries**: overseas@szepsivo.com
