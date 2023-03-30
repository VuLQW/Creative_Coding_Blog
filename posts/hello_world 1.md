---
title: Third Blog
publish_date: 31/03/2023
disable_html_sanitization: true
---
# 3rd Blog
<iframe width="576" height="366" src="https://editor.p5js.org/VuLQW/full/xNkGePPg0"></iframe>

The sketch was inspired by [Sketch 1](https://p5js.org/examples/simulate-particle-system.html). 
The falling animation was interesting it was very basic. I changed up the values of the vectors and 
its overall position. The speed is also increased so that it looks like its trying to fly somewhere. 
The shapes was changed and the colour was randomised to so that it felt sharped and it somewhat blended with the background.
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


# 2nd Blog
This is my first blog post!
<iframe width="576" height="366" src="https://editor.p5js.org/VuLQW/full/rSgtyXaV0"></iframe>

The sketch was inspired by [Sketch 2](https://p5js.org/examples/simulate-snowflakes.html).
The goal here was to follow the same structure as the original snow flake sketch,
however, I wanted to make the objects spin faster. This is to create the illusion that 
they're circling something in the middle even though there is nothing.
I also changed the colours and outline weight to stray away from the snowflake example.

```javascript
let snowflakes = []; // array to hold snowflake objects

function setup() { // runs once at the start
  createCanvas(576, 324); //creating a canvas
                          //576 pixels wide
                          //324 pixels tall
  
}

let word = function(){
  textSize(32);//the font size is 32 pixels
  stroke(255,255,255)// the stroke colour is RGB
                     // the red value = 255
                     // the green value = 255
                     // the blue value = 255
  fill(1) // colour of text is the shade of 1 which is black
  // the text shows 'RMIT Creative Coding Specialisation'
  //The x position of text is 30 pixels on the x axis
  // The y position of text is 30 pixels towards the y-axis
  text('RMIT Creative Coding Specialisation', 30, 30);
  
 
 
}
function draw() { //repeatedly draws after reference
  
  background(174,198,207); //puts a layer of background on canvas
                           //background color is rgb
                           // red is 174
                           // green is 198
                           // blue is 207
  word() // calling to the function word 

  
  let t = frameCount /10; // t refers to time
                          // every 10th of a frame count
                          // the object finishes its animation

  // creates random number of objects
  // defining i as the number 0
  // so if i is less than numbers random numbers of 0 to 5
  // add 2 towards i 
  for (let i = 0; i < random(5); i++) {
    
    snowflakes.push(new snowflake()); 
    // adds new objects (snowflakes) when the object ends
    
  }

  // creating a loop for the objectrs (flake)
  for (let flake of snowflakes) {
    flake.update(t); // updates the position of the snowflake
    flake.display(); // displays the elements of snowflakes 
  }

}

// creating a class for the snowflakes
function snowflake() {
  this.posX = 0; //  x position of the object is 0 pixels
  this.posY = random(-50, 0); 
  //y position of object randomises from -50 to 0  
  this.initialangle = random(0, 2 * PI); 
  // initial angle is determined through randomness of parameter
  // this ranges from 0 to 2xpi 
  this.size = random(2, 5); 
  //size of objects (snowflakes) ranges between 2 to 5

  // radius of snowflake spiral
  // this is so the snow flake spreads around the canvas
  // the radius is determined through the square root of parameter
  //parameter is randomly generated
  //rnage of parameter is half of width to 2 
  this.radius = sqrt(random(pow(width / 2, 2)));

  // x position follows a circle
  this.update = function(time) {
    let w = 0.3; 
    // declaring w as 0.3 
    let angle = w * time + this.initialangle;
    // declaring angle as the w multplied by time 
    // the initial angle is also added to the angle
    this.posX = width / 2 + this.radius * sin(angle);
    //the x position of object is dependant on:
    //half the width of canvas
    //plus the radius that is generated 
    //sin is also added to the angle to create pattern

    // allows the object to fall at different speeds 
    // the power of parameters are added to y position
    // this.size acts as the expression 
    // this.size has the power to 0.5
    // bigger the number means a faster fall 
    this.posY += pow(this.size, 0.5);

    // if the y position is larger than the height of canvas
    // objects are deleted
    if (this.posY > height) {
      let index = snowflakes.indexOf(this);
    //declaring index as snowflakes of the class 'this'
      snowflakes.splice(index, 1);
    //if this.posY > height is true 
    //the value of 1 is put into the arrays of the class 'this.'
    // Loops the animation 
    }
  };

  //creates the shape of the object 
  this.display = function() {
    ellipse(this.posX, this.posY, this.size);
      fill(250,253,15);// fills the canvas with rgb colour
                   // red is 250
                   // green is 253
                   // blue is 15
  stroke(1); //outline for the ellipse has the shade of 1
  // the position of the circle is in accordance to:
  // this.posX which constantly moves the x position
  // this.posY which constantly moves the y position
  // THE SIZE OF THE CIRCLE IS ALSO RANDOMLY GENERATED
  // SIZE IS RANDOMLY GENERATED BECAUSE OF THIS.SIZE
  };
}
```



