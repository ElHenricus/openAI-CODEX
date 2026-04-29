# Wiring (Raspberry Pi Pico W)

## Componentes
- 1x Raspberry Pi Pico W
- 1x Teclado matricial 4x4
- 12x LEDs
- 12x resistencias recomendadas (220Ω a 1kΩ)
- Cables Dupont

## Mapeo GPIO

### Teclado 4x4
| Señal | Pico W GPIO |
|---|---|
| R1 | GP26 |
| R2 | GP22 |
| R3 | GP21 |
| R4 | GP20 |
| C1 | GP19 |
| C2 | GP18 |
| C3 | GP17 |
| C4 | GP16 |

### LEDs
| LED | Pico W GPIO | Control por tecla |
|---|---|---|
| LED1 | GP11 | `1` |
| LED2 | GP10 | `2` |
| LED3 | GP9 | `3` |
| LED4 | GP8 | `4` |
| LED5 | GP7 | `5` |
| LED6 | GP6 | `6` |
| LED7 | GP5 | `7` |
| LED8 | GP4 | `8` |
| LED9 | GP3 | `A` |
| LED10 | GP2 | `B` |
| LED11 | GP28 | `C` |
| LED12 | GP27 | `D` |

## Comandos grupales
- `9`: enciende LED1..LED8
- `0`: apaga LED1..LED8
- `*`: enciende LED9..LED12
- `#`: apaga LED9..LED12

## Notas eléctricas
- En hardware real, colocar resistencia en serie con cada LED.
- Asegurar tierra común entre todos los componentes.
