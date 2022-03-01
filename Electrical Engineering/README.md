# Beginners’ Guide Into Electrical Engineering For Arduino And General Electronics:
This guide was written with the sole purpose of orienting absolute beginners into a safer,
more efficient way of handling electronic components and integrated systems. ***This guide 
does not tackle the subject of high voltage safety measures***; It is highly discouraged to deal 
with high voltages ( over approximately  50V) without proper training and experience. 
Such voltages can be extremely dangerous.  
## Table of Contents:
- Grounding.
- Short-circuits.
- Conventional Current.
- High Z state ( digitalRead() picks up random values from the push button)
- How do voltage dividers work?
- LEDS
- Actions to avoid when handling electronics.
- Useful pieces of advice.
- Useful Links

## Grounding:
As you’ve been probably told by one of our orientation members, the GND pin (Or the 0V pin) 
on the Arduino Uno board serves as a reference voltage for the other voltage  outputs that 
exist on the board. A simple way to explain this would be taking the act of measuring
distances of two different people as an example: you can only measure distances from
a certain point of reference. In the figure below,  the person on the left is 6m away 
from the tree, whilst the person on the right is 6m to the right of this same tree 
( or -6m away from the tree ). In our case, the ground is the tree and the voltages 
are the distances from this tree.  In short, the 5V pin on the Arduino only outputs 5V 
in regards to the Arduino’s ground. 
![References](https://user-images.githubusercontent.com/83831043/151665601-37a8c35f-78e7-4ac9-adf1-324ac425f05a.png)


Some of you might have concluded that the GND pin works 
the same way as a chassis ground ( the ground which was mentioned in previous High school courses). 
The chassis ground is used as a protective measure to protect from voltage leaks to the exterior metallic
boxes of home appliances ( it drives those lethal charges deep into the ground). The chassis ground is also
used as a reference voltage for the AC phases and is usually connected to the neutral wire.
The Ground represents the negative pole of our 5V Arduino supply. 
You’ll come to understand this better in the section about conventional current.

![chassis ground](https://user-images.githubusercontent.com/83831043/151665606-a54a4be0-bdf4-4a17-be24-e67fe7d09139.png)

Note: The ground symbols are sometimes used interchangeably. ( You can use one of them to represent the other types).
![types of ground](https://user-images.githubusercontent.com/83831043/151665612-86d9c10d-3755-419d-a74b-a66da281a28c.png)

## Short-circuit: (Court-circuit) (دارة مستقصرة  )
To fully understand this phenomenon, we need to understand two basic formulas of the Lumped model for electrical engineering
( a model is a group of formulas used for approximating real life phenomena.) .

Ohm’s Law:    V=R×I
R: Resistance (in ohms, symbol Ω )
I: Current (in Amps , symbol :A)
V: Voltage ( in Volts, symbol :V)


Example: ( made using Circuit lab , a decent tool for simulating real circuits in my opinion).
![circuit 1](https://user-images.githubusercontent.com/83831043/151665686-4b86570b-a651-49f3-a11d-8d637123dba9.png)

- Calculate the current flowing though R_Load (100 Ω ).
- Solution:

V=R×I ,    I=V/R , I=5/100 =0.05 A



You can think of the voltage as the PUSHING force ( potential energy) that DRIVES  the electrons through a rocky, jagged , 
harsh path ( resistor) and therefore causing a current to flow.  Do not memorize this formula and use it without fully grasping 
its significance (importance), this formula is the corner stone of electrical engineering.

Electrical Power formula: P= V×I

( this power represents the power absorbed by the component, this power is dissipated as ***heat*** in the case of a resistor.).

P: Power in watts ( W)
V: Voltage ( V)
I: Current (A)
  You can use ohm’s law to modify this formula as you see fit. Ex:
V=R×I……...1 , P=V×I…….2 ( by replacing 1 in 2 we get :)

P=I²×R
- Short-circuit Example:

![circuit 2](https://user-images.githubusercontent.com/83831043/151665841-deff5b27-7fda-49b8-bc7d-1d7631fb3f0d.png)

The image above represents an Ideal ( theoretical) short-circuit: in Real life all wires have some sort of resistance in addition to the internal resistance of the power supply 
( unwanted resistance that cannot be eliminate it i,e: we do not place it there on purpose , it just cannot be removed during the construction of the aforementioned
power supply).

![circuit3](https://user-images.githubusercontent.com/83831043/151665887-d159aa5f-89d1-477c-92af-6dac3496f29b.png)

This however is a much more accurate model for real short circuits.



We can often times combine resistors in a circuit into a single resistor to make the analysis significantly easier.
In this case the resistors are said to be in series ( the same current flows through them),  we can add their values up
and get our equivalent resistor. 
![Capture](https://user-images.githubusercontent.com/83831043/151666140-05f401ed-b29c-4c03-b302-c8cc0b4d089c.PNG)

Where Req=R1+R2.

This addition is only valid if the resistors are in ***series***, or in other words, share the same current.
The figure below gives us  insight on another case.

![Equivalent resistance](https://user-images.githubusercontent.com/83831043/151665931-83d45847-e312-4af3-a42a-1eb72019ac28.png)

(this connection is called: ***parallel*** connection of resistors).

for the real short circuit above, the analysis should be done as follows:

 ***Req***=1+1×10^-3=1.001 ohms

By applying the Power formula and ohm’s law we get :
     I=V/R=4.99A    , P=I²×Req=24.92W      
     
     (this value is significantly large and the Arduino 5V regulator which is the component responsible 
     for outputting the 5V CAN NOT reach this value.).

In the case of a certain 5V supply that can only output 1W of power for example, the said regulator will
certainly not be able to provide 24.92W, but instead will output 1W for a short period of time before turning into
charcoal and molten plastic, if it doesn’t have an adequate protection circuit that is. The heat is a result of the current flowing through 
the internal resistance of the regulator. Always keep in mind that current passing through a resistor causes heat generation. That is how most electrical
cooking plates work. Unfortunately for us,  our goal isn’t to make toxic heating plates.

(Electrical characteristics of the Arduino provided below in the Useful Links section.).


## Conventional Current And The Reason We Use It:
![current](https://user-images.githubusercontent.com/83831043/151666505-94b29ac8-863d-4ac1-a790-421ed86adabe.png)

The Conventional current is represented by the blue arrow while the electron flow is represented by the yellow circles with directional arrows. Physically speaking, it is the movement of electrons that we call “the current flow” . Nevertheless, we use “Conventional Current” in our circuit analysis even though it has no meaning in real terms. Conventional current ( defined by André-Marie ***Ampère***) was first thought to be the real direction of the flow of electrical energy until  J.J Thomson said otherwise. In order to avoid confusion, and to make certain electromagnetic and charge displacement phenomena more comprehensive, conventional current is used during circuit analysis. (ex: in the previous short-circuit example, it is much easier to think of the current as something that comes out of the sources and heads into the ground rather than electrons flowing from the ground to the supply.).

Note: We do use the flow of electrons to determine the potential causes of certain component faults (example: L-spikes). But overall, we rarely take it into account.


## Floating node/point(HIGH-Z):
Question:
 - What is the voltage Read at the digital input pin relative to GND when the switch SW2 is OFF?
![High Z](https://user-images.githubusercontent.com/83831043/151666607-cb0e6d6b-6f0a-425a-b28c-dba6bade705e.png)

Answer: We don’t know!

If you’ve answered zero in the previous question, then it means that you haven’t come across the concept of a floating node ( also called HIGH-Z and HIGH IMPEDANCE point). The voltage you are trying to measure is coming from a floating wire ( wire that is not connected to anything ) therefore the result of this measurement is bound to be pointless. This is an extremely common mistake that beginners commit when they start learning about switches. In real-life, this circuit will output random  values ( 1 then 0 then 1 again in a chaotic order). An easy fix for this problem would be to place a “Pull-down” resistor that “pulls” the voltage of the digital input pin to 0V whenever the push button is released. In other words, you get 0V output when the push button isn’t pressed.

![fix](https://user-images.githubusercontent.com/83831043/151666630-90d3dfbd-482d-47a1-b9f7-cbf8a5493b8e.png)


The 10K ohm resistor absorbs all the charges on the input and forces the voltage on the node to be 0V when SW1 is OFF.

Common questions: 
- Why don’t we just connect the pin to GND instead of placing a resistor?

- Because we would create a short-circuit whenever we press the button that way (no resistance between 5V and GND).

- How do we choose the value for the pull-down resistor?

- The value is chosen according to two criteria: the power that the source has to produce when the push button is pressed, and the effectiveness of the pull-down resistor. The effectiveness of the pull-down( also called the strength of the pull-down), and the power losses are inversely proportional: the bigger the resistance the harder it is for stray charges to move to the ground. However, a bigger resistance value means less power losses according to ohm’s law ( I=V/R , P=I²xR, notice that I is squared, which means that the decrease in its value will always be more significant on the value of power dissipation than the increase of the resistor value)). Most of the time, a 10K ohm resistor is used as a pull-down/up resistor* in 5V and 3.3V logic.

*Pull-up resistor: A resistor that “pulls” a certain node “UP” (to a High level 5V in our case).

*stray charges: charges that are picked up from something other than your power supply.

## Voltage Dividers:

Voltage dividers are simply a pair of resistors in series that divide the source voltage according to a certain resistance ratio. Since the same current flows through two resistors in series, we can easily find the voltage between the two resistors. 


![divider](https://user-images.githubusercontent.com/83831043/151666889-2ee97d7b-0739-4a5d-b220-f253e6818672.png)

In order to better understand voltage dividers, you’ll need to first understand that  resistors cause voltage drops in the circuit; the voltage at the output of the divider is guaranteed to be lower than the source voltage. That voltage drop can be measured using ohm’s law ***V(drop across resistor R2)=I×R2*** this voltage drop represents the electric potential* difference between the node at the higher potential and the node at the lower potential.
- Example:

V(drop across resistor R2)=5V – OUTPUT OF THE DIVIDER

(5V is at a higher potential than OUTPUT OF THE DIVIDER because of the voltage taken by the resistor called the voltage drop)

*Electric potential: we call voltages measured with respect to circuit ground “electric potential”. Sometimes the terms voltage and electric potential are used interchangeably.

A more general way to express ohm’s law would be :

Vh-Vl=R×I

Vh: High potential ( closer to source, farther from ground)

Vl: lower potential.

Question:How do we measure the output of a voltage divider?

- Answer: We first measure current, since it is the same for both resistors, in order to do so, we need to combine the resistors.
Rt=R1+R2

I=V/Rt =5/20k=0.25mA

then, we measure the voltage drop caused by R1:

Vh-Vl=R1×I

OUTPUT OF THE DIVIDER-0V=R1xI

OUTPUT OF THE DIVIDER=R1×I=0.25×10^(-3) ×10×10^3=2.5V

Alternatively, you can derive a general formula by using the same method
I=Vs/(R1+R2)

Vo=I×R1

Vo=Vs×R1/(R1+R2) 

Vs: source voltage
Vo: output of the divider

Since R1=R2:
Vo=Vs×R1/2R1=Vs/2 (2.5V in our case)

We can deduce that by modifying the values of R1 and R2 we can divide the voltage Vs to any value we want provided that it is not greater than Vs.

It is also important to note that voltage dividers are practically everywhere. for example, pontetiometers can be used as variable voltage dividers, in addition, some resistive sensors like LDRs (Photo-resistors) are commonly used in a voltage divider configuration so that whenever their resistance changes, so does the output voltage.

## Light emitting diodes ( LEDs):
- Questions:
How do I stop burning LEDs?

Answer:  by placing a ***well-matched*** resistor in series with them.
LEDs ( like any other type of diode (صمام ثنائي))  are active devices ( components that have two states or more: ON or OFF for the case of diodes).
Diodes -just like their name suggests- have two different terminals: Anode and cathode ( A and K). Whenever VA > Vk the diode conducts. This means that the diode only conducts in one direction of the current ( Anode connected to a higher potential than the cathode.).

The figure below uses switches to model the behavior of an IDEAL diode.

![diodes](https://user-images.githubusercontent.com/83831043/151667701-69ffb3c5-8d7d-4cd6-b4ac-234d63001dad.png)

A more realistic model would be the practical model, in which the diode only conducts if VA> VK + Vd

Vd = The voltage drop of the diode which is constant* regardless of the current unlike a resistor’s voltage drop.

Vd is also called the forward voltage.

To measure the right resistor value , we perform the following calculations:

Vh-Vl=R1xI

Vh= Vs-Vd

Vl=GND=0V

( You get Vd from a quick google search, not even a datasheet is required , Vd changes its value depending on the color of the light  emitted by the LED)

in the case of a red LED:

Vd=2V


 (Vs-Vd)-GND=R1xI
 
Another quick google search will help you find the right amount of current for a  red led (the current for a good lighting) ( 20mA ).

R1=(Vs-Vd)/I=150Ω

![d circuit](https://user-images.githubusercontent.com/83831043/151667705-b65ee5af-a6ae-4e71-ab95-7ac4dd94d405.png)

*Constant: Only approximately constant if VA>VK +Vd

## Things to avoid doing when handling Club equipment:



- Manually rotating the rotor of a Servo motor ( you are placing too much pressure on the potentio-meter/ encoder of those puny servos when you turn them manually)
- Manually rotating any motor while it is still connected to a circuit ( motors can create reverse voltages that can destroy your circuit).
- Using the A4988 (stepper motor driver) without asking club members about its vulnerabilities.
- Shorting any Arduino pin.
- Shorting any source to ground.
- Supplying the Arduino by a voltage higher than 12V and/or not on the Vin pin.
- Powering something very power demanding from the Arduino.
- Modifying the circuit while it is still powered on ( Short circuit risk).
- The arduino has an over- current protection that disconnects it digitally ( electronically) from your usb port when a current related fault occurs.Whenever you hear the sound of something disconnecting from the usb port, be aware that a short-circuit might have occured/is occuring.
- Not reading the datasheet of every component you put on your circuit EXTENSIVELY (less applicable for Arduino sensors, but is a good approach nonetheless).
- Not doing enough research on a given matter( IC , FIELD, CIRCUIT ...ETC) before trying to make it work ( Very important!)
- Building a huge complicated circuit directly without testing each section of it individually.
- Not being familiar/not using every debugging tool at your disposal ( Serial monitor in the case of Arduino).
- Not learning C or C++ while using Arduino IDE.
- Not consulting this guide when in doubt.
- Thinking this guide is all you need to know about electrical engineering.







## General Pieces of advice:
(This part is based off of my personal experience, and is by no means an absolute path towards success)

- It is always good to have a methodology (being organized) in electrical engineering.
- Try looking “under-the-hood” as much as possible: look for datasheets, try to understand every single functionality of the Arduino from a hardware perspective and low level programming perspective( meaning that you need to be able to write code without the basic Arduino functions analogRead() , digitalRead(), digitalWrite() at some point or at least understand how these functions work.
- “learn to learn”.
- Always simulate complicated circuits before implementing them, I personally use Ltspice but I recommend Everycircuit for beginners.
- Do not get tunnel vision, Arduino is a great piece of hardware that makes approaching electronics both less intimidating and less time consuming which can be attractive even for a seasoned engineer. That being said, do not limit yourself to just that: there are many more micro-controllers that offer  many more useful features, programming options and overall flexibility. I advise you to start programming only using the Atmega328p registers once you get familiar with Arduino ( it took me about a year to digest all its concepts ) and then slowly transition towards either the ESP32 MCUs or the STM32 MCUs – if you are interested in embedded systems that is- .






## Useful Links:
https://www.arduino.cc/en/pmwiki.php?n=Main/arduinoBoardUno
(Check technical Specs for the electrical characteristics of the Arduino)

https://www.youtube.com/channel/UCwd5VFu4KoJNjkWJZMFJGHQ ( For C and Embedded programming)
https://www.youtube.com/c/Electroboom
(Electrical Engineering)
https://www.youtube.com/c/greatscottlab
(General Electronics)
https://everycircuit.com/
(simulator)
You are in no way obliged to sit through every single video of these channels, what I advise you to do instead is watching the videos that are close to your center of interest at first and then gradually spreading your field of interest as you watch more videos.  

                                       -Written By Abayahia Hamou Zinedine ( aka Zinou)


