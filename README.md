# STM32 LCD Counter with Button and UART Output

## About this project

In this project, I used an STM32 microcontroller to build a simple counter system using a push button.

Every time I press the button:

* The number increases
* It is shown on the LCD
* The same number is converted into binary and sent through UART

This project helped me understand how input, processing, and output work together in embedded systems.

---

## Components used

* STM32 Nucleo board
* 16x2 LCD display
* Push button (on board - PC13)
* USB (for UART communication)

---

## Pin configuration

##  Button

* PC13 → Input
* Used to detect button press
* When pressed → reads LOW (0)

---

## LCD Connections

| LCD Signal | STM32 Pin |
| ---------- | --------- |
| D0         | PA10      |
| D1         | PB3       |
| D2         | PB5       |
| D3         | PB4       |
| D4         | PB10      |
| D5         | PA8       |
| D6         | PA9       |
| D7         | PC7       |
| RS         | PB6       |
| EN         | PA6       |
| RW         | GND       |

* LCD is used in **8-bit mode**
* Data is sent using GPIO pins

---

## How it works

1. System starts and LCD is initialized
2. Program continuously checks button state
3. When button is pressed:

   * Counter value increases
   * If value > 9 → reset to 0
   * Number is displayed on LCD
   * Number is converted into binary
   * Binary value is sent through UART

---

## Code logic (simple explanation)

* `num` → stores current number
* `lcd_data()` → sends character to LCD
* `lcd_command()` → sends command to LCD
* `Printdata()` → controls data pins

### Binary conversion:

```c
bin[0] = ((num >> 3) & 1) + '0';
bin[1] = ((num >> 2) & 1) + '0';
bin[2] = ((num >> 1) & 1) + '0';
bin[3] = ((num >> 0) & 1) + '0';
```

This converts number into 4-bit binary.

---

## Example

If button is pressed and:

* Number = 5

Then:

* LCD shows → `5`
* UART sends → `0101`

---

## Output

* LCD displays numbers from 0 to 9
* UART shows binary values of the same number
* Button controls the counting

---

## What I learned

* LCD interfacing using STM32
* GPIO input and output
* Button handling
* UART communication
* Binary conversion using bitwise operations
* Combining multiple peripherals

---

## Possible improvements

* Add proper button debouncing
* Use interrupts instead of polling
* Display full messages on LCD
* Increase range beyond 0–9

---

## Tools used

* STM32CubeIDE
* STM32 HAL Library

---

## Note

This project combines multiple concepts in one place, which helped me understand how real embedded systems work step by step.

This project is a combination of multiple basic concepts, and it helped me understand how real embedded systems handle input, processing, and output together.
