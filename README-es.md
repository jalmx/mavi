# 🔬 MaVI — Medidor Avanzado de Voltaje y Corriente

<div align="center">

![Estado](https://img.shields.io/badge/estado-WIP-yellow?style=flat-square)
![Licencia: GPLv3](https://img.shields.io/badge/Software-GPLv3-blue?style=flat-square)
![Licencia: CERN-OHL-S-2.0](https://img.shields.io/badge/Hardware-CERN--OHL--S--2.0-blue?style=flat-square)
![KiCad](https://img.shields.io/badge/KiCad-9.0-314CB0?style=flat-square)
![ESP32](https://img.shields.io/badge/MCU-ESP32-red?style=flat-square)
[![Docs](https://img.shields.io/badge/docs-mkdocs--material-purple?style=flat-square)](https://www.alejandro-leyva.com/mavi/)

> **Instrumento de código abierto para medición precisa de voltaje y corriente.**  
> ⚠️ _En desarrollo activo — esquemáticos y PCB en progreso, firmware aún no iniciado._

---

[🇬🇧 English version](README.md)

</div>

## ✨ Características

- **4 canales de voltaje** — rango de 0–50 V con impedancia de entrada de ~4 MΩ
- **Medición de corriente** — sensor de efecto Hall ACS712-5A (hasta 5 A)
- **Amplificador MCP6002** — ganancia ajustable (×10) con offset de 1.5 V
- **Protección contra sobretensión** — diodos de clamping 1N4148
- **ESP32** — microcontrolador de doble núcleo con ADC integrado
- **Pantalla LCD 16×02** — interfaz de usuario alfanumérica
- **Batería recargable** — 18650 Li‑ion + cargador TP4056
- **Registro en tarjeta SD** — almacenamiento de datos a bordo
- **Aviso sonoro** — buzzer piezoeléctrico
- **Caja imprimible en 3D** — diseño de carcasa personalizada
- **PCB en KiCad 9.0** — esquemático jerárquico (4 hojas), layout en progreso

## 📐 Diseño Electrónico

El hardware está diseñado con **KiCad 9.0** y organizado como proyecto jerárquico:

| Hoja | Estado |
|---|---|
| **Medición de voltaje** | ✅ Completado — red divisora, etapa de ganancia MCP6002, offset y clamping |
| **Microcontrolador (ESP32)** | 🟡 Pendiente |
| **Cargador (TP4056)** | 🟡 Pendiente |
| **PCB layout** | 🟡 En progreso |

> 📖 Análisis completo: [Diseño Electrónico](https://www.alejandro-leyva.com/mavi/electronic_design/)

### Cadena de Medición de Voltaje

```
  V_in (0–50 V)
      │
      ├─ 4 × 1 MΩ (divisor de alta impedancia)
      ├─ Diodos de clamping 1N4148
      ├─ Resistencia de sentido 10 kΩ → 130 mV @ 50 V
      └─ MCP6002 (ganancia ×10) → 1.3 V al ADC del ESP32
```

- **Impedancia de entrada:** ~4 MΩ  
- **Voltaje máximo medible:** 50 V  
- **Rango de entrada del ADC:** 0–1.3 V (dentro del rango 0–3.3 V del ESP32)  
- **Offset ajustable:** 1.5 V mediante divisor de voltaje + buffer

### Medición de Corriente

El sensor de efecto Hall **ACS712-5A** proporciona medición de corriente galvánicamente aislada hasta **5 A** con una sensibilidad de **185 mV/A**.

### Sistema de Alimentación

- **Batería:** Celda 18650 Li‑ion  
- **Cargador:** Módulo TP4056 (entrada USB 5 V)  
- **Regulación:** Convertidor boost a 5 V para el circuito

## 🖥️ Firmware

> 🚧 **No iniciado** — el directorio de firmware contiene solo placeholders.

Existen artefactos de diseño para:
- **Pantallas de UI** — maquetas en Excalidraw del flujo de la interfaz LCD  
- **Protocolo de comunicación** — diagrama de bloques de comunicación serie/I²C planeada  
- **Registro de datos** — almacenamiento en tarjeta SD planeado

## 📂 Estructura del Repositorio

```
📦 mavi/
├── 📁 .github/workflows/     # CI/CD — despliegue automático de docs a GitHub Pages
├── 📁 docs/                  # Sitio de documentación MkDocs
│   ├── 📄 index.md           # Página principal
│   ├── 📄 electronic_design.md  # Análisis de medición de voltaje
│   ├── 📄 case.md            # Diseño de carcasa e interfaz
│   ├── 📄 firmware.md        # Placeholder
│   ├── 📁 assets/            # Imágenes y recursos
│   ├── 📁 datasheets/        # Datasheets de componentes
│   └── 📁 firmware/          # Diagramas de UI y comunicación
├── 📁 schematic/             # Archivos de diseño KiCad
│   ├── 📄 mavi.kicad_pro     # Proyecto KiCad
│   ├── 📄 mavi.kicad_sch     # Esquemático principal (jerárquico)
│   ├── 📄 mavi.kicad_pcb     # Layout de PCB
│   ├── 📄 voltage.kicad_sch  # Hoja de medición de voltaje (completa)
│   ├── 📄 micro.kicad_sch    # Hoja de microcontrolador (pendiente)
│   └── 📄 cargador.kicad_sch # Hoja de cargador (pendiente)
├── 📁 firmware/              # Futuro código del firmware
│   └── 📄 index.md           # Placeholder
├── 📄 mkdocs.yml             # Configuración del sitio de documentación
├── 📄 pyproject.toml         # Proyecto Python (Poetry)
├── 📄 README.md              # Versión en inglés
├── 📄 README-es.md           # Este archivo
├── 📄 LICENSE.md             # GPLv3 (software)
└── 📄 HARDWARE_LICENSE.md    # CERN-OHL-S-2.0 (hardware)
```

## 🚀 Primeros Pasos

### Requisitos Previos

| Herramienta | Versión |
|---|---|
| [KiCad](https://www.kicad.org/) | 9.0 o posterior |
| [Python](https://www.python.org/) | 3.11+ |
| [Poetry](https://python-poetry.org/) | 2.4+ |

### Construir la Documentación Local

```bash
poetry install
poetry run mkdocs serve
```

Luego abre `http://localhost:8000` en tu navegador.

### Abrir el Diseño de Hardware

```bash
kicad schematic/mavi.kicad_pro
```

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Dado que el proyecto está en desarrollo temprano, siéntete libre de:

- Abrir *issues* para reportar bugs o sugerir características
- Enviar *pull requests* con mejoras al hardware o esbozos de firmware
- Ayudar a diseñar la carcasa (impresión 3D)
- Revisar el diseño electrónico

## 📄 Licencia

| Componente | Licencia |
|---|---|
| **Software y Firmware** | [GNU General Public License v3.0](LICENSE.md) |
| **Hardware (esquemáticos, PCB, carcasa)** | [CERN Open Hardware Licence Strongly Reciprocal v2.0](HARDWARE_LICENSE.md) |

## 👤 Autor

**Alejandro Leyva (Xizuth)**  

- GitHub: [@jalmx](https://github.com/jalmx)  
- Web: [alejandro-leyva.com](https://www.alejandro-leyva.com)  
- Email: jalm_x@hotmail.com

---

<div align="center">
  <sub>Hecho con ❤️ usando KiCad, MkDocs y ESP32</sub>
</div>
