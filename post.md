# Lab 3: Combinational Ramp Circuit Design

## Overview and Motivation

This week, our lab will involve both an analog and a digital component. We will be introduced to a way to get analog input, the potentiometer, and then we will use it, along with our Arduino, to light up a 7-segment display. By the end of this lab, we should be familiar with the voltage divider, the concept of a ramp circuit, and be comfortable with more complex combinational circuit.

Activities:
1. Get to know the voltage divider (potentiometer)
2. Use the Arduino to convert the potentiometer's analog signal into a 3-bit digital signal that represent the numbers 0 to 5 in binary.
3. Build a combinational circuit that, when given the 3-bit signal from the Arduino, display the numbers 0 to 5 on a 7-segment LED display.

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

## The 7-segment display

Before we start diving into the lab, we need to explain what a 7-segment display is and how it works. If you have ever taken a look at a number on your LCD alarm clock or on the pedestrian crossing timer, you will notice that the numbers are created using 7 light segments, hence the name "7-segment display". Our 7-segment display consists of 7 individually controlled LEDs (8 if you count the decimal point, but we will not be using it in this lab), labelled as follow:

<img width="279" alt="image" src="https://github.com/mlcourses/lab-3-blog-post-group1_cs281/assets/97915038/e29434cf-9af9-4234-b2d6-d55d4e02f269">

So when, for example, we want number 2 to light up, we would want the LEDs A, B, D, E and G to light up, but not C and F. For this lab, our goal is to be able to display the numbers 0 to 5, and the combination of LED segments for each number is as follow:

<img width="353" alt="image" src="https://github.com/mlcourses/lab-3-blog-post-group1_cs281/assets/97915038/109006e0-5c37-4228-a289-d90c110d24b8">

Out input will be a 3-bit numer that will represent the numbers 0 to 5 in binary (000, 001, 010 and so on). So now, our challenge is to take these 3 bits, and make them light up the corresponding combination of LEDs for each value. To accomplish this task, we will use a truth table.

## Truth Table

Let B<sub>2</sub>, B<sub>1</sub> and B<sub>0</sub> be our 3-bit number, with B<sub>2</sub> being the most significant bit. The truth table for our each of our LED segment is as followed, labelled like the figure above:

<img width="1273" alt="image" src="https://github.com/mlcourses/lab-3-blog-post-group1_cs281/assets/97915038/6bc27631-0fb6-4b0b-bc7f-3b43216d8aad">

After filling in the truth table, we can create an SOP expression for each LED. However, with 3 inputs and 6 numerical values, our expressions will be bulky. Hence, we will utilize some k-maps to simplify our SOP expressions. This step will make sure that our circuit will be as simple as possible and use as few IC chips as possible. Here are the SOP expressions for each LED after k-mapping:

<img width="1051" alt="image" src="https://github.com/mlcourses/lab-3-blog-post-group1_cs281/assets/97915038/c6dbed77-0b27-458c-b0ec-a07357e7a625">

<img width="589" alt="image" src="https://github.com/mlcourses/lab-3-blog-post-group1_cs281/assets/97915038/9e213565-09c7-4488-ad91-95ed2ef4e8e9">

<img width="988" alt="image" src="https://github.com/mlcourses/lab-3-blog-post-group1_cs281/assets/97915038/ce05cf86-0041-4ea6-ba53-90b99b344def">

## Logisim circuit and wiring diagram

Now that we have our minimal SOP expression, we can test out our circuit in Logisim before building it on the breadboard. The only difference is that the Logisim 7-segment display has 8 pins, while in real life it has 10, including 2 ground middle pins. We will keep that in mind when we build our circuit, but for now, the display in Logisim looks like this:

<img width="229" alt="image" src="https://github.com/mlcourses/lab-3-blog-post-group1_cs281/assets/97915038/119cc028-926e-449e-9b7e-276fd23b69d5">

The pins, from left to right, are: G, F, A, B (top 4 pins), E, D, C, and decimal point (unused) (bottom 4 pins).  Here is our complete circuit, with our 3 input bits:

<img width="1157" alt="7 segment logisim" src="https://github.com/mlcourses/lab-3-blog-post-group1_cs281/assets/97915038/612ce4f4-c049-4b08-818d-4da69aeb5828">

Note that among the OR gates, the 4th one from the top down is a 3-input OR gate. When we build the circuit on the breadboard, we will use 2 OR gates instead, since we don't have a 3-input OR gate. This brings the total of OR gates we will need to 6, which means we will have to use two 7432 IC chips (each only has 4 OR gates). The remaining 3 NOT gates and 3 AND gates will be implemented with a single 7404 and a 7408 IC chip. Here is the complete wiring diagram for our circuit, complete with wiring for power (WARNING: this one is a doozy, so wire carefully!)

![7 segment wiring](https://github.com/mlcourses/lab-3-blog-post-group1_cs281/assets/97915038/66178b6c-f9e9-4091-881b-89bfb106019e)

That is all the theoretical part! Let's move on to the next part.

## Voltage Divider / Potentiometer

Voltage Divider is an arragement of resistors configured to create a targer voltage. The equation to represent this is V = IR. V being voltage, I being the current, R being the resistance value of the resistor. A voltage divider consists of two resistors that are connected in series. The total resistance between these two is equal to R = R1 + R2 which is used to find the current I. Choosing our two resistance values allows us to pick any voltage V that we desire (between 0 and 5 volts).

<img width="484" alt="image" src="https://github.com/mlcourses/lab-3-blog-post-group1_cs281/assets/97915038/78df6f85-1073-428d-999a-fc83f6f802a9">

On our breadboard, the potentiometer is a voltage divider. A potentiometer is a varible resistor with an adjustable knob that lets us manually control the resistance. The breadboard we are using has both a 10k potentiometer and a 1k one (meaning the total sum of the resistance is 10kΩ and 1kΩ, respectively). For some reason, our 10k potentiometer was not functioning, so we will use the 1k potentiometer. While we will lose some granularity with our adjustment, ultimately our circuit will still be functional. We will wire the leftmost column of pin holes to GND, the rightmost column to +5V, and any of the 4 middle holes will be wired to our Arduino to take as input. The code below will be used to take the resistance from our potentiometer, convert it to a number from 0 to 5, then output that number through 3 digital pins as our 3 bit number:

```
const int potpin = 0;
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
dval = (val-317)/117; // normalizing factor
Serial.print("From Pot: ");
Serial.println(val);
Serial.print("Decimal Value Conversion: ");
Serial.println(dval);
//use bit ops to get each bit!
bitval = dval & 1;
digitalWrite(11,bitval); // signal A
dval = dval >> 1;
bitval = dval & 1;
digitalWrite(12,bitval); // signal B
dval = dval >> 1;
bitval = dval & 1;
digitalWrite(13,bitval); // signal C
delay(WAIT);
```

The ```potpin``` varible represents the analog input pin A0. The setup function has three pinMode function for pin 11,12 and 13 to set them as output pins to control LEDs or other digital devices. Also sets pin A0 as an input to read the analog value from the potentiometer. The loop function first defines variables ```val``` which is the anolog value from the potentiometer, ```dval``` which is the decimal value from the anolog value and ```bitval``` which is the binary representation of the decimal value.The extracted bits are then used to control three digital output pins, creating a binary representation of the original analog value.
## Testing

### Testing the potentiometer

Before we build our circuit, we need to test the potentiometer to make sure that our readings nad conversions are correct. If they are not, we will have to change the normalizing factor from above so that our Arduino can output numbers 0 to 5. The testing process and result is shown in this video:

https://github.com/mlcourses/lab-3-blog-post-group1_cs281/assets/97915038/3e2c8c99-3634-456e-b8ee-76d00dff53c8

### Building the circuit

Now that our potentiometer is calibrated, we are ready to build the circuit for our 7-segment display! We will be wiring exactly according to the wiring diagram above. one thing to add is that to protect the LEDs, we will wire a 1kΩ to each of the LED pin on our display. (Note: If you think the wiring diagram is a doozy, try looking at this one. If you intend to recreate this at home, follow the wiring diagram! One tip is to wire pin-by-pin, chip-by-chip and make sure that every connection from one pin is made before moving on to the next). Here is our assembled circuit:

![IMG_4267](https://github.com/mlcourses/lab-3-blog-post-group1_cs281/assets/97915038/743069e8-0185-4b6b-ab38-bae6c98ca31c)

The IC chips on the first column are the 7404 (top) and 7408 (bottom). The chips on the second column are both 7432 chips. The analog pin A0 is wired to the potentiometer, and the digital pins 11, 12 and 13 are where the Arduino outputs our 3 bits to be used as input for our circuit. The Arduino is also wired to GND on the board, so that they share the same sense of ground. Let's see our circuit in action!

https://github.com/mlcourses/lab-3-blog-post-group1_cs281/assets/97915038/8dda6306-27a4-4830-8ca3-39c9bde91ff3

## Conclusion

This lab has expanded our experience with combinational circuits by having us build a significantly more complex circuit compared to previous labs. We also got an introduction to the 7-segment display and the potentiometer, the latter being an implementation of the voltage divider. Due to the complexity of the lab, there was a significant amount of preparation involved, which helped us be more familiar with writing SOP expressions and using k-maps. Overall, this was a challenging but extremely interesting and helpful lab, and if you are interested in electronics or how computers work, you should definitely give it a go!


