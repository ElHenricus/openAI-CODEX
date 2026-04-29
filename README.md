# Pico W Keypad-to-LED Controller (Wokwi + Codex)

Este proyecto documenta y organiza una práctica de microcontroladores para **Raspberry Pi Pico W (RP2040)** usando un **teclado matricial 4x4** para controlar **12 LEDs**.

> **Nota importante de compatibilidad**  
> El código fuente provisto usa API estilo Arduino (`pinMode`, `digitalWrite`, `delay`, `Keypad.h`). Para ejecutarlo en un Pico W real se recomienda usar un core/framework compatible con esa API (por ejemplo Arduino-Pico). La lógica principal no fue alterada.

## 1) Bloques solicitados

### 1.1 `diagram.json` (inferencia compatible con el código proporcionado)

```json
{
  "version": 1,
  "author": "Codex (inferred from provided source code)",
  "editor": "wokwi",
  "parts": [
    { "type": "board-pico-w", "id": "pico", "top": 0, "left": 0, "attrs": {} },
    { "type": "wokwi-membrane-keypad", "id": "keypad", "top": -160, "left": 260, "attrs": {} },
    { "type": "wokwi-led", "id": "led1", "top": -220, "left": -220, "attrs": { "color": "red" } },
    { "type": "wokwi-led", "id": "led2", "top": -190, "left": -220, "attrs": { "color": "red" } },
    { "type": "wokwi-led", "id": "led3", "top": -160, "left": -220, "attrs": { "color": "red" } },
    { "type": "wokwi-led", "id": "led4", "top": -130, "left": -220, "attrs": { "color": "red" } },
    { "type": "wokwi-led", "id": "led5", "top": -100, "left": -220, "attrs": { "color": "red" } },
    { "type": "wokwi-led", "id": "led6", "top": -70, "left": -220, "attrs": { "color": "red" } },
    { "type": "wokwi-led", "id": "led7", "top": -40, "left": -220, "attrs": { "color": "red" } },
    { "type": "wokwi-led", "id": "led8", "top": -10, "left": -220, "attrs": { "color": "red" } },
    { "type": "wokwi-led", "id": "led9", "top": 20, "left": -220, "attrs": { "color": "blue" } },
    { "type": "wokwi-led", "id": "led10", "top": 50, "left": -220, "attrs": { "color": "blue" } },
    { "type": "wokwi-led", "id": "led11", "top": 80, "left": -220, "attrs": { "color": "blue" } },
    { "type": "wokwi-led", "id": "led12", "top": 110, "left": -220, "attrs": { "color": "blue" } }
  ],
  "connections": [
    ["pico:GP11", "led1:A", "green"], ["pico:GND.1", "led1:C", "black"],
    ["pico:GP10", "led2:A", "green"], ["pico:GND.1", "led2:C", "black"],
    ["pico:GP9", "led3:A", "green"], ["pico:GND.1", "led3:C", "black"],
    ["pico:GP8", "led4:A", "green"], ["pico:GND.1", "led4:C", "black"],
    ["pico:GP7", "led5:A", "green"], ["pico:GND.1", "led5:C", "black"],
    ["pico:GP6", "led6:A", "green"], ["pico:GND.1", "led6:C", "black"],
    ["pico:GP5", "led7:A", "green"], ["pico:GND.1", "led7:C", "black"],
    ["pico:GP4", "led8:A", "green"], ["pico:GND.1", "led8:C", "black"],
    ["pico:GP3", "led9:A", "green"], ["pico:GND.1", "led9:C", "black"],
    ["pico:GP2", "led10:A", "green"], ["pico:GND.1", "led10:C", "black"],
    ["pico:GP28", "led11:A", "green"], ["pico:GND.1", "led11:C", "black"],
    ["pico:GP27", "led12:A", "green"], ["pico:GND.1", "led12:C", "black"],

    ["pico:GP26", "keypad:R1", "orange"],
    ["pico:GP22", "keypad:R2", "orange"],
    ["pico:GP21", "keypad:R3", "orange"],
    ["pico:GP20", "keypad:R4", "orange"],

    ["pico:GP19", "keypad:C1", "purple"],
    ["pico:GP18", "keypad:C2", "purple"],
    ["pico:GP17", "keypad:C3", "purple"],
    ["pico:GP16", "keypad:C4", "purple"]
  ]
}
```

### 1.2 Código fuente (sin alterar lógica)

```cpp
#include <Keypad.h>

const uint8_t LEDS = 12;
const uint8_t ROWS = 4;
const uint8_t COLS = 4;

char keys[ROWS][COLS] = {
  { '1', '2', '3', 'A' },
  { '4', '5', '6', 'B' },
  { '7', '8', '9', 'C' },
  { '*', '0', '#', 'D' }
};

// Pins connected to LED1, LED2, LED3, ...LED12
uint8_t ledPins[LEDS] = { 11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 28, 27 };
uint8_t rowPins[ROWS] = { 26, 22, 21, 20 }; // Pins connected to R1, R2, R3, R4
uint8_t colPins[COLS] = { 19, 18, 17, 16 }; // Pins connected to C1, C2, C3, C4

Keypad keypad = Keypad(makeKeymap(keys), rowPins, colPins, ROWS, COLS);

void setup() {
  for (uint8_t l = 0; l < LEDS; l++) {
    pinMode(ledPins[l], OUTPUT);
    digitalWrite(ledPins[l], LOW);
  }
}

void loop() {
  char key = keypad.getKey();

  if (key != NO_KEY) {
    switch (key) {
      case '1': digitalWrite(ledPins[0], HIGH);
        break;
      case '2': digitalWrite(ledPins[1], HIGH);
        break;
      case '3': digitalWrite(ledPins[2], HIGH);
        break;
      case '4': digitalWrite(ledPins[3], HIGH);
        break;
      case '5': digitalWrite(ledPins[4], HIGH);
        break;
      case '6': digitalWrite(ledPins[5], HIGH);
        break;
      case '7': digitalWrite(ledPins[6], HIGH);
        break;
      case '8': digitalWrite(ledPins[7], HIGH);
        break;
      case '9':
        for (uint8_t l = 0; l < 8; l++) {
          digitalWrite(ledPins[l], HIGH);
        }
        break;
      case '0':
        for (uint8_t l = 0; l < 8; l++) {
          digitalWrite(ledPins[l], LOW);
        }
        break;
      case 'A': digitalWrite(ledPins[8], HIGH);
        break;
      case 'B': digitalWrite(ledPins[9], HIGH);
        break;
      case 'C': digitalWrite(ledPins[10], HIGH);
        break;
      case 'D': digitalWrite(ledPins[11], HIGH);
        break;
      case '*':
        for (uint8_t l = 8; l < 12; l++) {
          digitalWrite(ledPins[l], HIGH);
        }
        break;
      case '#':
        for (uint8_t l = 8; l < 12; l++) {
          digitalWrite(ledPins[l], LOW);
        }
        break;
    }
  }

  delay(10);
}
```

### 1.3 Descripción breve del diagrama

> El diagrama conecta un Raspberry Pi Pico W a un teclado matricial 4x4 (4 filas + 4 columnas) y 12 LEDs discretos. Las teclas numéricas `1..8` encienden LEDs individuales del primer banco, `9` enciende ese banco completo y `0` lo apaga. Las teclas `A..D` controlan LEDs individuales del segundo banco, mientras `*` enciende y `#` apaga el segundo banco completo.

## 2) Estructura propuesta del repositorio (C/C++)

```text
.
├── CMakeLists.txt
├── README.md
├── diagram.json
├── docs
│   ├── architecture.md
│   └── wiring.md
└── src
    └── main.cpp
```

## 3) Setup rápido

### Wokwi
1. Crear proyecto de Raspberry Pi Pico W.
2. Pegar `src/main.cpp` como sketch principal (entorno compatible Arduino API).
3. Pegar `diagram.json`.
4. Iniciar simulación.

### Hardware real (Pico W)
1. Cablear según `docs/wiring.md`.
2. Compilar y cargar con toolchain/framework compatible Arduino-style API para RP2040.
3. Abrir monitor serial si se agregan trazas (opcional; este código no imprime por serial).

## 4) Seguridad
- Este proyecto no utiliza Wi-Fi ni credenciales.
- Si luego se integra conectividad, usar archivo de configuración local ignorado por git (`.env`/`secrets.h`) y nunca commitear secretos.
