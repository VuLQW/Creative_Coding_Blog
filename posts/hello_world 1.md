---
title: First blog
publish_date: 31/03/2023
disable_html_sanitization: true
---
# 1st blog
<iframe width=576 height=366 src="https://editor.p5js.org/VuLQW/full/xNkGePPg0"></iframe>

The sketch was inspired by [particle system](https://p5js.org/examples/simulate-particle-system.html). 
The falling animation was interesting but was very basic. I changed up the values of the vectors and 
its overall position. The speed is also increased so that it looks like its trying to fly somewhere. 
The shapes was changed and the colour was randomised to so that it felt sharp and it somewhat blended with the background.
I also made the outline red to give contrast and gave the falling objects a range complement the random change in colour. 
```javascript
function setup() {       // runs one, at the start
  createCanvas(576, 324);// Creating a canvas 
                         // 574 pixels wide, and 324 tall
  system = new ParticleSystem(createVector(50, 50));
  // declaring system as the particle system which is also the vector
  // the system is placed 50 pixels on the x position
  // the system is placed 50 pixels on the y position 

}


function draw() { // repeatedly draws references after setup
  background(0,00,70) //fills in the background color (navy)
                       //RedGreenBlue values of 00, 00, 70
  word();
  system.addParticle();
  system.run();
 

}
//defining the letter word as a function

let word = function(){
  textSize(32);//the font size is 32 pixels
  stroke(255,255,255)// the stroke colour is RGB
                     // the red value = 255
                     // the green value = 255
                     // the blue value = 255
  // the text shows 'RMIT Creative Coding Specialisation'
  //The x position is 30 pixels on the x axis
  // The y position of text is 30 pixels towards the y-axis
  text('RMIT Creative Coding Specialisation', 30, 30);
 
 
}
// declaring 'particles' as function
// parameter of function is position
// position refers to the velocity of particle 
// position refers to acceleration of particle
// position refers to position of particle
// position refers to lifespan of particle
let Particle = function(position) { 
  
  // creating a vector to give direction to particles
  // parameters are the x and y values of vector
  // values of the x is 0.05 
  // value of y is 0.06
  this.acceleration = createVector(0.05,0.06);
  
  //the velocity is determined by randomness of determined vector
  // Intensity of velocity is determined by min/max(range) randomness
  // randomness of Vector's x value is -1 to 1
  // randomness of Vector's y value is -1 to 0
  this.velocity = createVector (random(-1,1), random(-1,0));
  
  //makes "this.position" the same as the command position.copy()
  //position.copy is declared later on the code
  this.position = position.copy();
  this.lifespan= 255;// lifespan equals to 255 frames
                     // takes 255 frames for particle to disappear  
}
// "Particle.prototype.run" is delcared as a function
// the function updates and displays particles
Particle.prototype.run = function(){
  this.update();
  this.display()
}

// This updates the position after previous commands 
Particle.prototype.update = function(){
  //the velocity accelerates following the values of "this.acceleration"
  this.velocity.add(this.acceleration); 
  //vthe position is then altered by the velocity and its values
  this.position.add(this.velocity);
  this.lifespan -= 2;//the particles disappear every 2 frames
}

//Displaying the actuial particles 
Particle.prototype.display = function(){
  //the stroke of the particle has an RGB value
  // 200 red, 1 green and 0 blue
  // the stroke follow "this.lifespan" so it fades when the lifespan ends
  stroke(200,1,0, this.lifespan);
  strokeWeight(2);//the weight of the outline/stroke of shape is 2
  // the shape is filled with random colours of RBG
  // the Red colour ranges from 0 to 59
  // the Green colour ranges from 0 to 2
  // the Blue colour ranges from 0 to 2
  // all values combine to make one colour but is randomly generated
  // colour also fades through "this.lifespan"
  fill(color(random(30), random(1), random(90)), this.lifespan);
  // Squares are created
  // the squares follow the "this.position.x/y" method
  //the positition constantly changes because of this
  //size of each square is 20 
  //the radius of each square is 1 
  square(this.position.x, this.position.y, 20, 1);
  
 
}
//the function sets the time the lifespan dies before threshold
Particle.prototype.isDead = function(){
// life span dies before 100 frames 
  return this.lifespan < 75;
}
//particleSystem is declared as a positional function
let ParticleSystem = function(position){
//this.position is also position.copy
//so this.origin equals this.position
  this.origin = position.copy();
//an array is created for "this.particles"
  this.particles = [];
}
//The position of particles commences after array of "this.particles" end
ParticleSystem.prototype.addParticle = function() {
    this.particles.push(new Particle(this.origin));
}


ParticleSystem.prototype.run = function(){
  //this runs the updating and display of the particles
  //declaring i to be the length of the particle 
  //i has a length that decreases by 1 pixel
  //if i is larger or equal to 0 
  //i will decrease by 2 pixels
  for (let i = this.particles.length -1; i>= 0; i--) {
  // defining p as i in an array
    let p = this.particles[i];
    p.run();//running p
    if (p.isDead()){ 
    // if the the lifespan of the particle dies when in array
    //the particles the array stops and restarts
      this.particles.splice(i, 1)
    }
  }
}
```