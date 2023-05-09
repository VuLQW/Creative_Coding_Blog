---
title: Third Blog
publish_date: 31/03/2023
disable_html_sanitization: true
abstract: wegnweogb
---

# 3rd blog

<iframe width="576" height="366" src="https://editor.p5js.org/VuLQW/full/5CBwSA5Uj"></iframe>

The sketch was inspired by [interaction wave maker](https://p5js.org/examples/interaction-wavemaker.html). 
I wanted to keep things sharp with this sketch and keep the animations proportionate. To achieve this I decided to create squares
than to keep circles. It thought it would be interesting to incorporate a sharp square and make multiple make a flowing and 
wavy like pattern. Outlines were added to further highlight the trail with a little touch of purple to break the black and white 
aesthetic. The waves moves in accordance to the position of the mouse where keeping the mouse off the canvas will enable the squares 
to flow by itself. The frames switch to 30fps on the canvas when the mouse doesn't hover. I did this so the trails and actual pattern
of the squares could be emphasised instead of having the sketch go by really quick. 

```javascript
let t = 0; // time variable

function setup() {
  createCanvas(600, 600);
  noStroke();
  fill(40, 200, 40);
}

function draw() {
  background(10, 10); // translucent background (creates trails)

  // make a x and y grid of ellipses
  for (let x = 0; x <= width; x = x + 30) {
    for (let y = 0; y <= height; y = y + 30) {
      // starting point of each circle depends on mouse position
      const xAngle = map(mouseX, 0, width, -4 * PI, 4 * PI, true);
      const yAngle = map(mouseY, 0, height, -4 * PI, 4 * PI, true);
      // and also varies based on the particle's location
      const angle = xAngle * (x / width) + yAngle * (y / height);

      // each particle moves in a circle
      const myX = x + 20 * cos(2 * PI * t + angle);
      const myY = y + 20 * sin(2 * PI * t + angle);

      ellipse(myX, myY, 10); // draw particle
    }
  }

  t = t + 0.01; // update time
}
```




