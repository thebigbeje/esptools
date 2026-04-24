```markdown
# ⚡ ESP32/8266 Development & Deployment Toolchain

O suită de automatizare pentru ciclul de dezvoltare al microcontrolerelor ESP32 și ESP8266. Acest set de instrumente facilitează compilarea, gestionarea sistemelor de fișiere (LittleFS/SPIFFS) și deployment-ul rapid prin Serial sau OTA.

## 🛠️ Componente Incluse

### 1. `esp-dev-toolchain.zsh`
Orchestratorul principal care automatizează întregul workflow:
- **Compilare:** Interfață peste `arduino-cli` cu logging detaliat al erorilor.
- **Filesystem Tools:** Generare automată de imagini binare pentru date (`/data`).
- **Deployment:** Suport pentru flashing prin port serial sau rețea (OTA).
- **Monitor:** Lansare instantanee a monitorului serial cu baudrate configurabil.

### 2. `gen_esp32part.py`
Utilitar pentru manipularea tabelelor de partiții ESP32. Permite convertirea între formatul CSV (uman lizibil) și formatul binar utilizat de bootloader-ul ESP-IDF.

### 3. `espota.py`
Scriptul standard pentru deployment Over-The-Air. Permite actualizarea firmware-ului și a sistemului de fișiere de la distanță, fără conexiune fizică USB.

## 🚀 Utilizare Rapidă

### Configurare
Creează un fișier `project.conf` în rădăcina proiectului:
```bash
board="esp32"
board_fqbn="esp32:esp32:esp32da"
port="/dev/ttyUSB0"
ip="192.168.1.100"
auth="parola_ota"
```

### Comenzi comune
```bash
# Compilare și upload serial
./esp-dev-toolchain.zsh --compile --upload

# Generare sistem de fișiere și upload OTA
./esp-dev-toolchain.zsh --filesystem --upload-ota

# Monitorizare serială
./esp-dev-toolchain.zsh --monitor
```

## 📋 Dependențe
- `arduino-cli`
- `python3` (pentru esptool, espota)
- `mklittlefs` / `mkspiffs`
- `fping` (pentru verificarea stării online a dispozitivelor)

## 🛡️ Security & Reliability
- **Validare Automată:** Scriptul verifică integritatea variabilelor de mediu și formatul adreselor IP înainte de execuție.
- **Error Handling:** Compilarea este întreruptă imediat dacă sunt detectate erori, prevenind flash-uirea unui binar corupt.
- **Safe OTA:** Include logică de așteptare (wait-for-online) pentru a asigura stabilitatea conexiunii înainte de transferul datelor.

---
*Dezvoltat pentru optimizarea workflow-ului de Engineering în proiecte de automatizare și IoT.*
```
