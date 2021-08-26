---
layout: post
title: MAKER DESIGN=> Building a 25 microbit led display
description: Building a macrobit display
summary: Building a 25 microbit led display
tags: MAKER DESIGN
minute: 5
---

![x25 microbit display](/assets/images/code/MB/mbx25.png)

# Building a macro:bit

The BBC micro:bit is a mini-controller that can be programmed to do almost any task. It has a built-in accelerometer, radio transmitter / bluetooth, thermometer, compass, two programmable buttons and a 5 by 5 LED display.

This tiny device is the best learning tool to introduce our new generations of programmers to the fascinating interconnected future of IOT-The Internet of Things.

## Building a 5x5 grid of micro:bits

The challenge was to design a simple 5x5 grid of microbits who would receive data through radio waves from one micro:bit, and recreate the light patterns of the single unit to a bigger grid of 25 micro:bits.

![x25 microbit display](/assets/images/code/MB/silver.jpg)

## [=> SEE THE VIDEO](https://www.youtube.com/watch?v=Qwjg-GyTLRw&feature=youtu.be)

## Code

> [Sender Code](https://makecode.microbit.org/44062-46375-02900-64749)

```js
// Javascript code with syntax highlighting.
function sendShape () {
    for (let x = 0; x <= 4; x++) {
        for (let y = 0; y <= 4; y++) {
            send_to_group += 1
            if (led.point(x, y)) {
                radio.setGroup(send_to_group)
                radio.sendNumber(1)
                basic.pause(10)
            } else {
                radio.setGroup(send_to_group)
                radio.sendNumber(0)
                basic.pause(10)
            }
        }
    }
    send_to_group = 0
}
input.onButtonPressed(Button.A, function () {
    chooseShape()
    sendShape()
})
input.onButtonPressed(Button.B, function () {
    createShape()
    sendShape()
})
input.onGesture(Gesture.Shake, function () {
    basic.clearScreen()
    basic.showIcon(IconNames.Heart)
})
function chooseShape () {
    choice = Math.randomRange(1, 4)
    if (choice == 1) {
        basic.showIcon(IconNames.Skull)
    } else if (choice == 2) {
        basic.showIcon(IconNames.Ghost)
    } else if (choice == 3) {
        basic.showIcon(IconNames.Snake)
    } else {
        basic.showIcon(IconNames.Cow)
    }
}
function createShape () {
    basic.clearScreen()
    for (let index = 0; index < 25; index++) {
        led.plot(Math.randomRange(0, 4), Math.randomRange(0, 4))
    }
}
let choice = 0
let send_to_group = 0
basic.showIcon(IconNames.Heart)
send_to_group = 0
}
```

> [Receiver Code](https://makecode.microbit.org/48079-81697-88730-98123)

```js
// Javascript code with syntax highlighting.
radio.onReceivedNumber(function (receivedNumber) {
    inner_light = 0
    basic.clearScreen()
    if (receivedNumber == 1) {
        for (let x = 0; x <= 4; x++) {
            for (let y = 0; y <= 4; y++) {
                led.plot(x, y)
            }
        }
    }
    if (receivedNumber == 0) {
        for (let x = 0; x <= 4; x++) {
            for (let y = 0; y <= 4; y++) {
                led.unplot(x, y)
            }
        }
    }
    if (receivedNumber == 2) {
        basic.clearScreen()
    }
})
function blink () {
    while (inner_light == 1) {
        led.toggle(2, 2)
        basic.pause(100)
    }
}
input.onButtonPressed(Button.A, function () {
    inner_light = 0
    led.plot(2, 2)
    basic.clearScreen()
})
let inner_light = 0
radio.setGroup(25)
basic.clearScreen()
inner_light = 1
blink()
}
```
