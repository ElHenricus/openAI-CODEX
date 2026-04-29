# Arquitectura de firmware

## Objetivo funcional
Controlar 12 salidas digitales (LEDs) desde un teclado matricial 4x4 usando reglas de mapeo directas por tecla.

## Estructura
- `src/main.cpp`
  - Define constantes de tamaño (`LEDS`, `ROWS`, `COLS`).
  - Declara mapa de teclas (`keys`).
  - Declara arreglos de pines (`ledPins`, `rowPins`, `colPins`).
  - Inicializa objeto `Keypad`.
  - `setup()`: configura GPIO de LEDs y estado inicial en LOW.
  - `loop()`: lee tecla y ejecuta `switch` con acciones de encendido/apagado.

## Flujo lógico
1. Inicialización de pines de salida para LEDs.
2. Lectura periódica de teclado.
3. Si hay tecla válida:
   - Acción unitaria (encender un LED), o
   - Acción por lote (encender/apagar un banco de LEDs).
4. Pequeño retardo (`delay(10)`) para estabilizar el ciclo.

## Dependencias
- `Keypad.h` (escaneo de teclado matricial).
- API estilo Arduino (`pinMode`, `digitalWrite`, `delay`).

## Criterio de no modificación de lógica
Se conservó exactamente la lógica de control original; solo se reorganizó el repositorio y se añadió documentación técnica.
