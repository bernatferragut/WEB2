---
layout: post
title: GENERATIVE DESIGN | The Big 0
description: A course in Generative Art
summary: Creating algorithmic art with canvas html5
tags: GENERATIVE DESIGN
minute: 25
---
# Generative Design - The Big 0
![generative art course](/assets/images/code/GA2/GA2-1.png)

This compilation of programmed works represented 2 years of generative based art explorations. The exhibition was made online over a free web platform and the jury the web itself through social media. This series made my art enter into a pure coding and programming direction and opened me to the study of Computational thinkning as the origins of modern digital arts.

> Art Work & Exhibition:
## [=> ONLINE GENERATIVE DESIGN EXHIBITION](https://bernat-generative-art.surge.sh/)

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="pdvmWZ" data-user="elbernat" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/elbernat/pen/pdvmWZ">
  Generative Art -Big O</a> by Bernat Ferragut (<a href="https://codepen.io/elbernat">@elbernat</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

## The Code

```javascript
// JS Code by Bernat Ferragut 2017
// selecting your Canvas5
let canvas = document.querySelector('canvas');
// console.log(canvas);

// resizing your canvas
canvas.height = window.innerHeight;
canvas.width = window.innerWidth;

// canvas execution context
let ctx = canvas.getContext('2d');
// console.log(ctx);

// Utility function to get random values
function randomIntegerFromRange (min, max) {
    return Math.floor(Math.random() * ( max - min + 1) + min);
}

// Utility function to get random colors
const randomColorArray = ['#004358', '#1F8A70', '#BEDB39', '#FFE11A', '#FD7400']; // From Kuler
function randomColors(randomColorArray) {
    return randomColorArray[randomIntegerFromRange(0,4)];
}
// console.log(randomColors(randomColorArray));

// particle object creation
function Particle (x, y, radius, color) {
    // variables
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.color = color;
    this.radians =  Math.random() * Math.PI * 2; // random angle spawner (0-360)
    this.velocity = 0.01; // how fast we change
    this.distanceFromCenter = { x:  randomIntegerFromRange(30, 120),y:  randomIntegerFromRange(90, 120)}; // Coolest option 
    // this.distanceFromCenter = randomIntegerFromRange(250, 300);
    // update function
    this.update = function() {
        // Behaviour1: move points over time
        this.radians += (this.velocity);
        // Behaviour2: circular motion position
        this.x = x + (Math.cos(this.radians)) * this.distanceFromCenter.x * 3;
        this.y = y + (Math.sin(this.radians)) *  this.distanceFromCenter.y * 3;
        // We store the last particle positon
        const lastPoint = { x: this.x, y: this.y };
        // Draw > pass lastPoint
        this.draw(lastPoint);
    };
    // draw function
    this.draw = function(lastPoint) {
        ctx.beginPath();
        ctx.strokeStyle = this.color;
        ctx.lineWidth = this.radius;
        ctx.lineCap = 'round';
        ctx.moveTo(lastPoint.x, lastPoint.y);
        ctx.lineTo(this.x, this.y);
        ctx.stroke();
        ctx.closePath();
    };
}

// vars
let particles =[];
let nParticles = 2000;
// implementation
function init() {
    for (let i = 0; i < nParticles; i++) {
        const radius = randomIntegerFromRange(1,3);
        const color = randomColors(randomColorArray);
        particles.push(new Particle(canvas.width / 2, canvas.height / 2, radius, color));
    }
}
//init call
init();
console.log(particles);

// animation loop
function animate() {
    // ctx.clearRect(0 ,0 , canvas.width, canvas.height);
    // Trail effect
    ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    // For each
    particles.forEach( function(particle) { particle.update() });
    // Creates a Loop
    requestAnimationFrame(animate);
}
// animate call
animate();

```
## [=> ONLINE GENERATIVE DESIGN EXHIBITION](https://bernat-generative-art.surge.sh/)