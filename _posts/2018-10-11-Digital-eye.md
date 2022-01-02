---
layout: post
title: GENERATIVE DESIGN=> The algorithmic eye code
description: A course in Generative Art
summary: Creating algorithmic art with canvas html5
minute: 25
---
# Generative Design - DIGITAL EYE
![generative art course](/assets/images/code/GA1/GA1-1.png)

This compilation of programmed works represented 2 years of generative based art explorations. The exhibition was made online over a free web platform and the jury the web itself through social media. This series made my art enter into a pure coding and programming direction and opened me to the study of Computational thinkning as the origins of modern digital arts.

> Art Work & Exhibition:
## [=> ONLINE GENERATIVE ART EXHIBITION](https://bernat-generative-art.surge.sh/)

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="KywrXP" data-user="elbernat" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/elbernat/pen/KywrXP">
  Generative Art - Canvas Eye</a> by Bernat Ferragut (<a href="https://codepen.io/elbernat">@elbernat</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

## The Code

```javascript
// JS - Code by Bernat Ferragut 2017
// selecting your Canvas HTML5
let canvas = document.querySelector('canvas');
// console.log(canvas);

// resizing your canvas
canvas.height = window.innerHeight;
canvas.width = window.innerWidth;

// canvas execution context
let ctx = canvas.getContext('2d');

// Utility function to get random values
function randomIntegerFromRange (min, max) {
    return Math.floor(Math.random() * ( max - min + 1) + min);
}

// Utility function to get random colors
const randomColorArray = ['#FF530D', '#E82C0C', '#FF0000', '#E80C7A', '#FF0DFF']; // From Kuler
function randomColors(randomColorArray) {
    return randomColorArray[randomIntegerFromRange(0,5)];
} 

// particle object creation
function Particle (x, y, radius, color) {
    // variables
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.color = color;
    this.radians =  Math.random() * Math.PI * 2; // random angle spawner (0-360)
    this.velocity = 0.01; // how fast we change
    // this.distanceFromCenter = { x:  randomIntegerFromRange(90, 120),y:  randomIntegerFromRange(90, 120)}; // Coolest option 
    this.distanceFromCenter = Math.sin(randomIntegerFromRange(250, 300)) *380;
    // update function
    this.update = function() {
        // Behaviour1: move points over time
        this.radians += Math.random((this.velocity));
        // Behaviour2: circular motion position
        this.x = x + (Math.cos(this.radians)) * this.distanceFromCenter;
        this.y = y + (Math.sin(this.radians)) *  this.distanceFromCenter;
        // We store the last particle positon
        const lastPoint = { x: this.x, y: this.y };
        // Draw > pass lastPoint
        this.draw(lastPoint);
    };
    // draw function
    this.draw = function(lastPoint) {
        ctx.beginPath();
        // first time with an arc
        // ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2, false);
        // second time with a line
        ctx.strokeStyle = this.color;
        ctx.lineWidth = this.radius;
        ctx.lineCap = 'round';
        ctx.moveTo(lastPoint.x, lastPoint.y);
        ctx.lineTo(this.x, this.y);
        ctx.stroke();
        // ctx.fillStyle = this.color;
        // ctx.fill();
        ctx.closePath();
    };
}

// vars
let particles =[];
let nParticles = 250;
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
    ctx.fillStyle = 'rgba(0, 0, 0, 0.025)';
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    // For each
    particles.forEach( function(particle) { particle.update() });
    // Creates a Loop
    requestAnimationFrame(animate);
}
// animate call
animate();
```
## [=> ONLINE GENERATIVE ART EXHIBITION](https://bernat-generative-art.surge.sh/)