# 🔬 MaVI — Advanced Voltage and Current Meter

<div align="center">

![Status](https://img.shields.io/badge/status-WIP-yellow?style=flat-square)
![License: GPLv3](https://img.shields.io/badge/Software-GPLv3-blue?style=flat-square)
![License: CERN-OHL-S-2.0](https://img.shields.io/badge/Hardware-CERN--OHL--S--2.0-blue?style=flat-square)
![KiCad](https://img.shields.io/badge/KiCad-9.0-314CB0?style=flat-square)
![ESP32](https://img.shields.io/badge/MCU-ESP32-red?style=flat-square)
[![Docs](https://img.shields.io/badge/docs-mkdocs--material-purple?style=flat-square)](https://www.alejandro-leyva.com/mavi/)

> **Open-source instrument for precise voltage and current measurement.**  
> ⚠️ _Actively developed — schematics and PCB in progress, firmware not yet started._

---

[🇪🇸 Versión en español](README-es.md)

</div>

## ✨ Features

- **4 voltage channels** — 0–50 V range with ~4 MΩ input impedance
- **Current sensing** — ACS712-5A hall-effect sensor (up to 5 A)
- **MCP6002 op-amp** — adjustable gain (×10) with 1.5 V offset
- **Overvoltage protection** — 1N4148 clamping diodes
- **ESP32** — dual-core microcontroller with built-in ADC
- **LCD 16×02 display** — alpha-numeric user interface
- **Rechargeable battery** — 18650 Li‑ion + TP4056 charger
- **SD card logging** — onboard data storage
- **Piezo buzzer** — audible alerts
- **3D-printable enclosure** — custom case design
- **KiCad 9.0 PCB** — hierarchical schematic (4 sheets), PCB layout in progress

## 📐 Electronic Design

The hardware is designed with **KiCad 9.0** and organised as a hierarchical project:

| Sheet | Status |
|---|---|
| **Voltage measurement** | ✅ Detailed — divider network, MCP6002 gain stage, offset & clamping |
| **Microcontroller (ESP32)** | 🟡 Placeholder |
| **Charger (TP4056)** | 🟡 Placeholder |
| **PCB layout** | 🟡 In progress |

> 📖 Full analysis (in Spanish): [Electronic Design](https://www.alejandro-leyva.com/mavi/electronic_design/)

### Voltage Measurement Chain

```
  V_in (0–50 V)
      │
      ├─ 4 × 1 MΩ (high-impedance divider)
      ├─ 1N4148 clamping diodes
      ├─ 10 kΩ sense resistor → 130 mV @ 50 V
      └─ MCP6002 (gain ×10) → 1.3 V to ESP32 ADC
```

- **Input impedance:** ~4 MΩ  
- **Max measurable voltage:** 50 V  
- **ADC input range:** 0–1.3 V (within ESP32's 0–3.3 V)  
- **Adjustable offset:** 1.5 V via voltage divider + buffer

### Current Measurement

The **ACS712-5A** hall-effect sensor provides galvanically isolated current measurement up to **5 A** with a sensitivity of **185 mV/A**.

### Power System

- **Battery:** 18650 Li‑ion cell  
- **Charger:** TP4056 module (5 V USB input)  
- **Regulation:** Boost converter to 5 V for the circuit

## 🖥️ Firmware

> 🚧 **Not started** — the firmware directory contains placeholders only.

Design artefacts exist for:
- **UI screens** — Excalidraw mockups of the LCD interface flow  
- **Communication protocol** — block diagram of planned serial/I²C communication  
- **Data logging** — SD card storage planned

## 📂 Repository Structure

```
📦 mavi/
├── 📁 .github/workflows/     # CI/CD — auto-deploy docs to GitHub Pages
├── 📁 docs/                  # MkDocs documentation site
│   ├── 📄 index.md           # Landing page
│   ├── 📄 electronic_design.md  # Voltage measurement analysis (Spanish)
│   ├── 📄 case.md            # Enclosure & UI design
│   ├── 📄 firmware.md        # Placeholder
│   ├── 📁 assets/            # Images & resources
│   ├── 📁 datasheets/        # Component datasheets
│   └── 📁 firmware/          # UI & communication diagrams
├── 📁 schematic/             # KiCad hardware design files
│   ├── 📄 mavi.kicad_pro     # KiCad project
│   ├── 📄 mavi.kicad_sch     # Top-level schematic (hierarchical)
│   ├── 📄 mavi.kicad_pcb     # PCB layout
│   ├── 📄 voltage.kicad_sch  # Voltage measurement sheet (complete)
│   ├── 📄 micro.kicad_sch    # Microcontroller sheet (placeholder)
│   └── 📄 cargador.kicad_sch # Charger sheet (placeholder)
├── 📁 firmware/              # Future firmware source
│   └── 📄 index.md           # Placeholder
├── 📄 mkdocs.yml             # Documentation site config
├── 📄 pyproject.toml         # Python project (Poetry)
├── 📄 README.md              # This file
├── 📄 README-es.md           # Spanish version
├── 📄 LICENSE.md             # GPLv3 (software)
└── 📄 HARDWARE_LICENSE.md    # CERN-OHL-S-2.0 (hardware)
```

## 🚀 Getting Started

### Prerequisites

| Tool | Version |
|---|---|
| [KiCad](https://www.kicad.org/) | 9.0 or later |
| [Python](https://www.python.org/) | 3.11+ |
| [Poetry](https://python-poetry.org/) | 2.4+ |

### Build the Documentation Locally

```bash
poetry install
poetry run mkdocs serve
```

Then open `http://localhost:8000` in your browser.

### Open the Hardware Design

```bash
kicad schematic/mavi.kicad_pro
```

## 🤝 Contributing

Contributions are welcome! Since the project is in early development, feel free to:

- Open issues for bugs or feature suggestions
- Submit pull requests with hardware improvements or firmware stubs
- Help design the enclosure (3D printing)
- Review the electronic design

## 📄 License

| Component | License |
|---|---|
| **Software & Firmware** | [GNU General Public License v3.0](LICENSE.md) |
| **Hardware (schematics, PCB, enclosure)** | [CERN Open Hardware Licence Strongly Reciprocal v2.0](HARDWARE_LICENSE.md) |

## 👤 Author

**Alejandro Leyva (Xizuth)**  

- GitHub: [@jalmx](https://github.com/jalmx)  
- Web: [alejandro-leyva.com](https://www.alejandro-leyva.com)  

---

<div align="center">
  <sub>Built with ❤️ using KiCad, MkDocs, and ESP32</sub>
</div>
