---
title: 1st Blog
publish_date: 31/03/2023
disable_html_sanitization: true
---
# 1st Blog

<iframe width="576" height="366" src="https://editor.p5js.org/VuLQW/full/5CBwSA5Uj"></iframe>

The sketch was inspired by [interaction wave maker](https://p5js.org/examples/interaction-wavemaker.html). 
The falling animation was interesting it was very basic. I changed up the values of the vectors and 
its overall position. The speed is also increased so that it looks like its trying to fly somewhere. 
The shapes was changed and the colour was randomised to so that it felt sharped and it somewhat blended with the background.
I also made the outline red to give contrast and gave the falling objects a range complement the random change in colour. 

```javascript
let t = 0; // declaring the time variable which is t
           // t is takes in the value of 0


function setup() { // runs once, at the start 
  createCanvas(576, 324); // create a canvas
                          // 576 pixels wide
                          // 324 pixels tall
  
  frameRate(30) // canvas runs at 30 frames per second
}

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

function draw() { //repeatedly draws reference after setup
  background(10, 10); //makes the background translucent
                      //makes trail effect

  // creates a grid for the squares 
  for (let x = 0; x <= width; x = x + 30) {
    // declaring x as 0 
    // the value of x always has to be:
    // - less than width
    // - or equal to width
    // value of 30 is constantly added to x
    
    for (let y = 0; y <= height; y = y + 30) {
    // declaring y as 0 
    // the value of y always has to be:
    // - less than width
    // - or equal to width
    // value of 30 is constantly added to y 
      
      const xAngle = map(mouseX, 0, width, -4 * PI, 4 * PI, true);
//the xAngle become a consant
// alters the starting point of x position 
// the x position depend on position of mouse
// the x position of mouse has a range of 0 and canvas width
// moving mouse on x axis will change squares target position
// target position moves square along range of: -4PI and 4PI
      
      const yAngle = map(mouseY, 0, height, -4 * PI, 4 * PI, true);
//the yAngle become a consant
// alters the starting point of y position 
// the y position depend on position of mouse
// the y position of mouse has a range of 0 and canvas height
// moving mouse on y axis will change squares target position
// target position moves square along range of: -4PI and 4PI
      
      const angle = xAngle * (x / width) + yAngle * (y / height);
// angle of x and y is combined to work together
// it is under the constant angle
// values that were previously created in const yAngle change
// the x and y value is divided by width (x) and height (y)

//all particles move in a circular motion
      const myX = x + 20 * cos(2 * PI * t + angle);
      const myY = y + 20 * sin(2 * PI * t + angle);
// The particles movement on x axis follow cos function
// The particles movement on y axis follow sin function

      square(myX, myY, 20); // draws particle as square 
                            // size of square is 20
      stroke(100,20,80) //outline of sqaure is added
                        //outline of square is purple
                        //outline uses rgb values
                        //red = 100
                        //green = 80
      strokeWeight(0.1) // thickness of outline is 0.1
    }
    word()
  }

  t = t + 0.01;
  // updates time
  // 0.01 is constantly added to time every frame
  // slows down the time for square to loop
  // occurs when mouse is not over canvas
}



