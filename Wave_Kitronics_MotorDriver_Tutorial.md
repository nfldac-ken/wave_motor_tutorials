
```package

pxt-kitronik-motor-driver=github:kitronikltd/pxt-kitronik-motor-driver#v0.0.8

```




# Microbit Wave Motor Control with Driver board : Create the code.



## Add the set up code to the on start block
This is executed when the Microbit is reset.


### Add the code to create some variables and give them a value
This is used to control the start and stop for the motor


### Make the variables. 

Make a variable by selecting  ``||Variables.make a variable()||``

> and clicking on the black **Make a Variable...** box

>> Give it the name **startStop**

Make a second variable by selecting  ``||Variables.make a variable()||``

> Give it the name  **speedFactor**

And a third variable by selecting  ``||Variables.make a variable()||``

> Giving it the name  **speed**




### Set up the variables. 

Find the  ``||Variables.variables set()||`` instruction 

and place it in the on start block.

use the drop down arrow and select the ``||start_Stop||`` variable name

> check it is set to **0** in the **white circle** 


place a second **set** variable instruction from 
 ``||Variables.make a variable()||``

use the drop down arrow **v** to select **speedFactor** 

> set **speedFactor** to **2** 


These are the initial values for these variables that are 
used to control the motor. 


### Add the display

drag and drop a  ``||basic:show leds||`` into the **onstart** block

clicking on the squares to turn them white to create a tick shape


```blocks


let startStop = 0
startStop = 0
let speedFactor = 2
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

> use the dropdown arrow **v** to select the **star_Stop** variable

Change the value in the **white circle** to **1**

>>When at a value of one, 
this variable is used later to instruct the code to run the motor.


### Button B, stop the motor

Right click on the **on button A pressed** function 
and select **Duplicate** to create a copy.

> drop this into a clear space on the screen. 

Use the drop down arrow **v** to change **A** to **|B**  
> the block will go from grey to purple. 

### Inside the on button B pressed function


Change the value of **set startStop** in the white circle to 0 

> a value of zero stops the motor.

### Add a status display. 

Drag and drop a  ``||basic:show leds||`` inside at 
the top of the **on button A pressed ** block 

> clicking on the squares to turn them white to create an 
upward arrow shape to indicate that the motor is going to turn. 


Drag and drop a  ``||basic:show leds||`` inside at 
the top of the **on button B pressed ** block 

> clicking on the squares to turn them white to create a 
a square with a diagonal line accross it 
to indicate that the motor is going to turn. 

> look at the lightbulb hint to see how these might look.


``` blocks

input.onButtonPressed(Button.A, function () {
    startStop = 1
    basic.showLeds(`
        . . # . .
        . # # # .
        # . # . #
        . . # . .
        . . # . .
        `)
    
})
input.onButtonPressed(Button.B, function () {
     startStop = 0
     basic.showLeds(`
        # . # # #
        # # . . #
        # . # . #
        # . . # #
        # # # . #
        `)

})



```


## Add code to the Forever block
This will run continuously and drive the motor when requested 


### Add a logic function instruction 

Drag and drop a  **loops** ``||loops.while do||`` 
into the **forever** block 


### Set up the control of the loop block

Drag and drop a  ``||Logic.logic()||``   **0 =v 0** 
operator into the box with the same **vee** shaped ends at 
the top of the **while** instruction. 

> this is the top shape. 

In the  ``||Variables.variables()||`` menu

 > drag the **red oval** shape named **startStop** onto the **white circle**
 after the word **while** 

after the **=** set the value in the **white circle** to **1** 

### Add some code inside the logic while instruction 

From the  ``||Variables.variables()||`` menu drag 
and drop **variables.set** and place it inside the green loop function


> use the dropdown arrow **v** to select the **speed** variable. 

Add a ``||Math.math()||`` operator, **0 = v 0** 

> this is at the top.  

>> drop it onthe **white circle** after thew word **to**




Add a ``||Math.math()||`` operator, **0 / v 0** 

> this is second from the bottom. 

>> drop it on the first **white circle** after the word **to**


From the  ``||Variables.variables()||`` menu **Your Variables** drag 
and drop **speedFactor** and place it onto the first **white circle** 

>> change the second **white circle** to the value **20** 

>> and the last **white circle** to the value **5**


This sets a value for the variable **speed** based on another variable 
**speedFactor** and lets us use a more convenient 
range of 0-100 for its value 


### Motor instruction. 

In the **Motor Driver** menu drag a  ``||kitronik_motor_driver.motorOn()||`` 
instruction and place it under the **set speed** instruction 

> check it is set to **motor 1 v**

This instruction talks to the motor driver board 

In the  ``||Variables.variables set()||`` menu

 drag a copy of the **Your Variables** named **speed** onto the white circle
 after the word **speed** 

The value of **speed** determines how fast the motor turns 


### Add a short delay

 From the ``||basic||`` menu 
 
 drag a copy of ``||basic.pause()||`` and drop it in below
 the **motor** instruction 

 check the delay value is **100 mS**

 > This lets the hardware settle between updates.


### Stop the motor

From the **Motor Driver** menu drag a 
 ``||kitronik_motor_driver.motorOff()||`` 

 > and put it outside of the green **while do** but inside the blue 
 **forever** block 

 >> this stops the motor when the variable **startStop** is set to **0** 


```blocks

basic.forever(function () {
    while (startStop == 1) {
        speed = speedFactor / 20 + 5
        kitronik_motor_driver.motorOn(kitronik_motor_driver.Motors.Motor1, kitronik_motor_driver.MotorDirection.Forward, speed)
        basic.pause(100)
    }
    kitronik_motor_driver.motorOff(kitronik_motor_driver.Motors.Motor1)
})


```


## Add a every funtion block to drive the display 
This allows us to see some of what is going on in the code

### From the Loops menu

drag and drop a  ``||loops.every||`` ``||loop||`` 
into a blank space

Check the value in the white drop down box is ``||500||`` ms




### From the **Basic** menu 
drop a  ``||basic.shownumber()||`` instruction 
inside the **every** function.


### From the **Math** menu 

Find the ``||Math.math()||`` operator, **round v 0** 

> this is at the bottom. 

>> drop it on the **white circle** 


Find a ``||Math.math()||`` operator, **0 / v 0** 

> this is second from the bottom. 

>> drop it on the **white circle**




### From the **variables** menu 

Drag a copy of the **Your Variables** named **speedFactor** 
 onto the first **white circle** 


Change the second **white circle** value to **10**

> This shows a representation of the speed factor on the MicroBit 
display.


``` blocks

loops.everyInterval(500, function () {
    basic.showNumber(Math.round(speedFactor / 10))
})

```




## Try it out
Check your code looks just like the light bulb hint, then 

Get some help to make the connections to the test motor,
the motor contoller, 
and its power supply.

> then click ``|Download|`` to try your code out on the connected MicroBit
to see what it does.


### Make some observations and write them down 

What happens to the MicroBit display?

> and when the buttons are pressed, 

What happens to the motor and the display? 


> Is it working correctly?

### Make some measurements to see if the speed is correct 

When the motor speed is measured, is it running at the speed 
that you are trying to achieve? 

> If not, you will need to modify the code to change the speed ......



```blocks
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . . # . .
        . # # # .
        # . # . #
        . . # . .
        . . # . .
        `)
    startStop = 1
})
input.onButtonPressed(Button.B, function () {
    basic.showLeds(`
        # . # # #
        # # . . #
        # . # . #
        # . . # #
        # # # . #
        `)
    startStop = 0
})
let speed = 0
let startStop = 0
basic.showLeds(`
    . . . . .
    . . . . #
    . . . # .
    # . # . .
    . # . . .
    `)
startStop = 0
let speedFactor = 2
loops.everyInterval(500, function () {
    basic.showNumber(Math.round(speedFactor / 10))
})
basic.forever(function () {
    while (startStop == 1) {
        speed = speedFactor / 20 + 5
        kitronik_motor_driver.motorOn(kitronik_motor_driver.Motors.Motor1, kitronik_motor_driver.MotorDirection.Forward, speed)
        basic.pause(100)
    }
    kitronik_motor_driver.motorOff(kitronik_motor_driver.Motors.Motor1)
})
```

## Changing the motor speed 
.

Find the **on start** function block 

> and find the **set speedFactor** instruction 

>> change the value of the number in the **white circle** to **5** 


###  Send the updated code to the Microbit 
by clicking ``|Download|`` 

What has changed? 


### Take a new speed measurement 
And then adjust the variable **speedFactor** to get as close as you can 
to your target revolutions per mininte (rpm) 

> this may take several attempts.....


```blocks


let startStop = 0
startStop = 0
let speedFactor = 5
basic.showLeds(`
    . . . . .
    . . . . #
    . . . # .
    # . # . .
    . # . . .
    `)

})



```