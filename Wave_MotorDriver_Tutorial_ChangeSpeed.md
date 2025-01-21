
```package

pxt-kitronik-motor-driver=github:kitronikltd/pxt-kitronik-motor-driver#v0.0.8

```

```template

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

# Microbit Wave Motor Control with Driver board : Change the speed 

## See what the code does
Get some help to make the connections to the test motor,
the motor contoller, 
and its power supply.

> then click ``|Download|`` to try your code out on the connected MicroBit
to see what it does.


### Make some observations and write them down 

What happens to the MicroBit display?

> and when the buttons are pressed, 

What happens to the motor and the display? 



### Make some measurements to see if the speed is correct 

When the motor speed is measured, is it running at the speed 
that you are trying to achieve? 

> If not, you will need to modify the code to change the speed ......



## Changing the motor speed 
.

Find the **on start** function block 

> and find the **set speedFactor** instruction 

>> change the value of the number in the **white circle** to **5** 


###  Send the updated code to the Microbit 
by clicking ``|Download|`` 

> What has changed? 


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