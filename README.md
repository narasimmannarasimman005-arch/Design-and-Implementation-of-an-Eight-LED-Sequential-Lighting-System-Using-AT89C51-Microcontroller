# Design-and-Implementation-of-an-Eight-LED-Sequential-Lighting-System-Using-AT89C51-Microcontroller
Design and Implementation of an Eight-LED Sequential Lighting System Using AT89C51 Microcontroller using Proteus


# Aim
To design and implement an 8-LED sequential lighting system (chaser light effect) using the AT89C51 Microcontroller by shifting logic states across an 8-bit I/O port with software-generated time delays

# Apparatus Required
1. AT89C51 Microcontroller (8051 architecture)
2. Light Emitting Diodes (LEDs) × 8
3. Resistors (330 Ω) × 8 (Current-limiting resistors for LEDs)
4. Crystal Oscillator (11.0592 MHz) × 1
5. Capacitors (33 pF) × 2 (For oscillator stability)
6. Capacitor (10 µF) × 1 & Resistor (10 kΩ) × 1 (For the hardware reset circuit)
7. 5V DC Power Supply
8. Keil µVision IDE & Proteus Simulation Software (or hardware programmer/breadboard)

# Algorithm
1. Start the execution loop.
2. Configure Port 1 (or Port 2) as an output port by initializing it to a known state.
3. Initialize the sequence data with the binary value 0x01 (00000001 in binary), which lights up only the first LED (connected to pin P1.0).
4. Send the data out to the designated microcontroller port pins.
5. Call the Delay function to hold the current configuration visible to the human eye.
6. Shift the logic bit left by one position (data = data << 1) to target the next LED pin.
7. Check if the shift overflows past the 8th LED. If the binary value exceeds 0x80 (10000000), reset the sequence tracking byte back to 0x01.
8. Repeat steps 4 through 7 in an infinite loop

# DIAGRAME:
<img width="760" height="532" alt="image" src="https://github.com/user-attachments/assets/80a7e3fc-1549-4afc-ac32-0966b9ee58d3" />


# Program (Embedded C):


#include <reg51.h> // Include standard 8051 register definitions

// Function Prototype for the time delay
void delay(unsigned int time);

void main(void) {
    unsigned char led_pattern;
    
    while(1) { // Infinite loop for ongoing sequence
        led_pattern = 0x01; // Initial state: 00000001 (LED 1 ON)
        
        while(led_pattern != 0x00) {
            P1 = led_pattern;       // Output the pattern to Port 1 pins
            delay(30000);           // Hold the pattern visible
            led_pattern = led_pattern << 1; // Shift left (e.g., 00000001 becomes 00000010)
        }
    }
}

// Time delay generation function
void delay(unsigned int time) {
    unsigned int i, j;
    for(i = 0; i < time; i++) {
        for(j = 0; j < 10; j++); // Nested loop to burn clock cycles
    }
}

# Program Result
Simulation & Hardware Output: Upon running the code, the 8 LEDs connected to Port 1 turn ON and OFF one after another in a linear sequence (P1.0 → P1.1 → P1.2 \[\dots \] → P1.7

