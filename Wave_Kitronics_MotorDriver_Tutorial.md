```package

pxt-kitronik-motor-driver=github:kitronikltd/pxt-kitronik-motor-driver#v0.0.8

```





# Microbit Wave Motor Control with Driver board



## Add the set up code to the on start block
This is executed when the Microbit is reset.


### Add the code to create some variables and give them a value
This is used to control the start and stop for the motor

Make a variable by selecting  ``||Variables.make a variable()||``

and clicking on the black Make a Variable... box

give it the name ``||start_Stop||``

do the same to add another variable ``||potentiometer_1||``


Find the  ``||Variables.variables set()||`` sub-block

and place it in the on start block.

use the drop down arrow and select the ``||start_Stop||`` variable name

check it is set to ``||0||``


Make a second variable by selecting  ``||Variables.make a variable()||``

and clicking on the black Make a Variable... box

give it the name ``||potentiometer_1||``

do the same to add another variable ``||potentiometer_1||``

check it is set to ``||0||``


### Add the display

drag and drop a  ``||basic:show leds||`` into the ``||basic:onstart||`` island block

clicking on the squares to turn them white to create a tick shape


```blocks

let potentiometer_1 = 0
let start_Stop = 0
start_Stop = 0
potentiometer_1 = 0
basic.showLeds(`
    . . . . .
    . . . . #
    . . . # .
    # . # . .
    . # . . .
    `)

```





## Create the Start and Stop buttons
to control the motor start and stop.

### Button A, start the motor

Add an ``||input.onButtonPressed(a)||`` from the input menu
placing it in a clear space





From the  ``||Variables||`` menu drag
and drop ``||variables.set()||`` and place it inside the ``||on button A||``
function.

use the dropdown arrow to select the ``||start_Stop||`` variable

Change the value in the white circle to ``||1||``

When at a value of one, 
this variable is used later to instruct the code to run the motor.


### Button B, stop the motor

Right click on the ``||on button B||`` function
 and select ``||Duplicate||`` to
create a copy.

Use the drop down arrow to change ``||A||`` to ``||B||``,
the block will go from grey to purple.
Inside the ``||on button B||`` function


Inside the ``||on button B||`` function 
right click and copy the ``||set||`` sub-function

and place it inside the ``||on button B||`` function

use the dropdown arrow to select the ``||start_Stop||`` variable

Change the value in the white circle to ``||0||``

A value of zero stops the motor.

``` blocks

input.onButtonPressed(Button.A, function () {
    start_Stop = 1
})
input.onButtonPressed(Button.B, function () {
    start_Stop = 0
})



```


## Add code to the Forever block
This will run continuously and drive the motor


### Add a logic function sub-block

drag and drop a  ``||loops.while||`` ``||loop||`` 
into the ``||basic:forever||`` island block


use the dropdown arrow to select the ``||Potetiometer_1||`` variable



### Set up the control of the loop block

drag and drop a  ``||Logic||``  ``||logic:||``  ``||0 = 0||`` 
operator into the same shaped box at the
 top of the ``||while||`` sub-function replacing the ``||false||`` operator.

In the  ``||Variables.variables set()||`` menu

 drag a copy of the your variables ``||start_Stop||`` onto the white circle
 after the word ``||while||``

after the ``||=||`` set the value to ``||1||``


### Add some code inside the logic while sub-block

From the  ``||Variables||`` menu drag
and drop ``||variables.set()||`` and place it inside the green loop function


use the dropdown arrow to select the ``||Potetiometer_1||`` variable


### In the ``||Motor Driver||`` ``||kitronik_motor_driver.motorOn()||`` menu

 drag a copy of the  ``||motor on direction||`` sub-block
 onto the white circle
and place it inside the loop block


check it is set to ``||motor 1||``



In the  ``||Variables.variables set()||`` menu

 drag a copy of the your variables ``||Potetiometer_1||`` onto the white circle
 after the word ``||speed||``

 This writes the value read from the potentiometer
 to drive the motor controller

### Add a short delay

 From the ``||basic||`` menu 
 
 drag a copy of ``||basic.pause()||`` and drop it in below
 the analog write sub-block

 type in a delay time of 10 mS

 This lets the hardware settle in between updates.





```blocks

basic.forever(function () {
    while (start_Stop == 1) {
        potentiometer_1 = pins.analogReadPin(AnalogReadWritePin.P1)
        kitronik_motor_driver.motorOn(kitronik_motor_driver.Motors.Motor1, kitronik_motor_driver.MotorDirection.Forward, potentiometer_1)
        basic.pause(10)
    }
})


```


## Add a every funtion block to drive the display

### From the Loops menu

drag and drop a  ``||loops.every||`` ``||loop||`` 
into a blank space

Check the value in the white drop down box is ``||500||`` ms



Find the  ``||Variables.variables set()||`` sub-block

and place it in the ``||every||`` loop block.

use the drop down arrow and select the ``||potentiometer_1||`` variable name


In the  ``||Variables.variables()||`` menu

 drag a copy of the your variables ``||Potetiometer_1||`` onto the white circle
 after the word ``||to||``

Add a ``||basic.showNumber()||`` below the ``||set||`` sub-block


Find the ``||Math||``  ``||math.0 / 0|``|   operator and drag it 

onto the white circle after the word ``||number||``


 Drag a copy of the your variables ``||Potetiometer_1||`` 
 onto the left hand white circle before the  ``||/||`` symbol

Change the righ hand white circle after the  ``||/||`` symbol
to 100

### The code above reads the analog input pin and saves its value.

Places it into the potentiometer_1 variable (which is 0 to 1023),
 then displays the value, divided by 100 (now 0 to 10)
on the MicroBit display. It does this every 500 mSeconds.


``` blocks

loops.everyInterval(500, function () {
    potentiometer_1 = pins.analogReadPin(AnalogReadWritePin.P1)
    basic.showNumber(potentiometer_1 / 100)
})


```




## Try it out
Check your code looks just like the hint then

Get some help to make the connections to the test motor,
the motor contoller,
and its power supply.

click ``|Download|`` to try your code out on the connected MicroBit
to see what it does.

What happens to the motor as the MicroBit display changes?

W

Is it working correctly?






```blocks

input.onButtonPressed(Button.A, function () {
    start_Stop = 1
})
input.onButtonPressed(Button.B, function () {
    start_Stop = 0
})
let potentiometer_1 = 0
let start_Stop = 0
start_Stop = 0
potentiometer_1 = 0
basic.showLeds(`
    . . . . .
    . . . . #
    . . . # .
    # . # . .
    . # . . .
    `)
loops.everyInterval(500, function () {
    potentiometer_1 = pins.analogReadPin(AnalogReadWritePin.P1)
    basic.showNumber(potentiometer_1 / 100)
})
basic.forever(function () {
    while (start_Stop == 1) {
        potentiometer_1 = pins.analogReadPin(AnalogReadWritePin.P1)
        kitronik_motor_driver.motorOn(kitronik_motor_driver.Motors.Motor1, kitronik_motor_driver.MotorDirection.Forward, potentiometer_1)
        basic.pause(10)
    }
})


```

