# Lab 3: Combinational Ramp Circuit Design

Please write a blog post describing your lab here.

This is just an example of how you might structure your blog post, feel free to edit as you wish. For example, you might divide the lab into different sections each with their own intro, instructions, results, and takeaways. Please see the rubric for details on how the post will be evaluated.

## Overview and Motivation
This week we'll be using an analog input to display a number on a 7-segment display.
## Materials
1)PB-503 Breadboard
2)5161AS 7-Segment Display
3)Arduino
4)7404,7408 and 7432 IC Gates
5)Resistors
## Project Steps
1) Fill in the truth table in Figure 4 to indicate the outputs for each LED segment in the 7-segment display.
2) Use the truth table in Figure 4 to make an SOP expression for each output.
3) Use the same truth table to make a K-map for each output and then find a minimal boolean expression
for each output.
4) Use logisim to design a boolean circuit for the minimized functions. Test the circuit.
5) Understand Voltage Divider
6) Build Circuit

## Truth Tables

To build this circuit we first have to start with some preparation. This includes building a truth table to create SOP expression for each output. This is important for the design of the circuit. The digital signal representing a decimal value from 0 to 5, and controls the illumination of LEDs based on this value. The goal is to create a truth table that specifies the behavior of the circuit for all possible input combinations.

...



After filling in the truth table and creating SOP expressions, we will used the same tables to make K-maps for each output. K-Maps allow us to simplify the SOP expressions to minimize the amount of ICs we use and to create easier circuits overall.



...



Now we are able to visualize the circuit we are going to make with the help of the K-Maps




...






## Voltage Divider

Voltage Divider is an arragement of resistors configured to create a targer voltage. The equation to represent this is V = IR. V being voltage, I being the current, R being the resistance value of the resistor. A voltage divider consists of two resistors that are connected in series. The total resistance between these two is equal to R = R1 + R2 which is used to find the current I. Choosing our two resistance values allows us to pick any voltage V that we desire (between 0 and 5 volts).


....

To do this we will use a potentiometer. A potentiometer is a varible resistor with an adjustable knob that lets us manually control the resistance. The breadboards we are using has both a 10k potentiometer and a 1k one meaning the total sum of the resistance is 10kΩ and 1kΩ. After connecting the leftmost column to GND, rightmost to 5V and using one of the middle columns to our arduino we are ready to build our circuit.



....

The photo above shows how we will connect all the parts of lab to generate the number on the 7-segment display.

```const int potpin = 0;
const int WAIT = 1000; // 1 second delay
void setup () {
Serial.begin(9600);
pinMode(11,OUTPUT);
pinMode(12,OUTPUT);
pinMode(13,OUTPUT);
pinMode(potpin,INPUT);
}
void loop () {
int val;
int dval;
int bitval;
val = analogRead(potpin);
dval = val/171; // normalizing factor-->adjust this to get the range you want
Serial.print("From Pot: ");
Serial.println(val);
Serial.print("Decimal Value Conversion: ");
Serial.println(dval);
//use bit ops to get each bit!
bitval = dval & 1;
digitalWrite(11,bitval); // signal C
dval = dval >> 1;
bitval = dval & 1;
digitalWrite(12,bitval); // signal B
dval = dval >> 1;
bitval = dval & 1;
digitalWrite(13,bitval); // signal A
delay(WAIT);
```
## Testing

## Conclusion




