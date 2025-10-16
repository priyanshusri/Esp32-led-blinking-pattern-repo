In my implementation of the said LED pattern I avoided
using the usual pinMode() and digitalWrite() functions for controlling the LEDs. Instead, I
configured the pins using the ESP-IDF gpio_config_t structure and drove the LEDs directly
through the ESP32 GPIO registers (GPIO.out_w1ts and GPIO.out_w1tc). This made the code
closer to the hardware and also more efficient, since it changes multiple pins in a single
instruction.
For the button input of my implementation, I enabled the internal pull-up resistor and used an
external interrupt on the falling edge. In order to make the button more reliable, I added a
software debounce using esp_timer_get_time(), so accidental multiple detections from
bouncing contacts are filtered out. Each valid button press cycles through a state machine that
changes the LED pattern (off → led1 → led2 → led3 → all).
The main special thing about my solution is that it uses register-level LED control plus an
interrupt-driven button instead of simple polling or Arduino functions. This matches real
embedded system practices and makes the program more responsive and efficient.

## Subheader

Git tutorial

## Local development

1. Open index.html in your browser.