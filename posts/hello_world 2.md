---
title: Second Blog
publish_date: 31/03/2023
disable_html_sanitization: true
---

# 2nd Blog

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



