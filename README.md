# miqu0971_9103_tut5
# Part 1：Imaging Technique Inspiration

##  Thousand Histories
Suzann Victor’s “[**A Thousand Histories**](https://gajahgallery.com/exhibition/a-thousand-histories/)” is composed of thousands of Fresnel lenses that refract images from the colonial era, creating a fragmented, multidirectional visual experience.  
  
When I first saw this work at the Art Gallery of New South Wales, I was unaware of its historical context, but it immediately captivated me. The way the lenses refracted and blurred the images compelled me to pause and examine the images behind them more closely. This very form, paradoxically, makes viewers more focused and perceptive as they engage with the work.
![A Thousand Histories](https://storage.ghost.io/c/16/43/16435400-f27e-4b41-b5f7-d0c24f5ce4de/content/images/size/w2000/2025/07/City-Lantern--Detail--1.JPG)

# Part 2：Coding Technique Exploration
##  Self Portrait -test
Yvani’s “[**Self Portrait -test**](https://openprocessing.org/sketch/2418839)” presents a visual effect similar to that of “A Thousand Histories”. The work reconstructs the image through constantly shifting particles, offering viewers a fragmented and blurred visual experience. This visual effect bears a certain resemblance to the refraction and displacement effects produced by Fresnel lenses.
![Self Portrait-test](https://cdn.phototourl.com/free/2026-05-07-4a10d9a5-6029-4f99-8206-c40fec847812.jpg)
```JavaScript
let bubbles = [];
let self, c;
let offsetX = 400; // Offset to shift the image 600 pixels to the right

function preload() {
  self = loadImage('yv01.png');
}

function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  
  // Initial reduced number of bubbles
  for (let i = 0; i < 300; i++) {
    bubbles.push(new colorbubble());
  }
}

function draw() {
  background(0); // Set the background to black

  // Generate fewer bubbles per frame
  for (let i = 0; i < 50; i++) {
    bubbles.push(new colorbubble());
  }

  // Update and display each bubble
  for (let colorbubble of bubbles) {
    colorbubble.move();
    colorbubble.delete();
    colorbubble.display();
  }
}

class colorbubble {
  constructor() {
    // Set the initial position to the center of the canvas
    this.pos = new p5.Vector(width / 2, height / 2);
    this.vel = new p5.Vector(0, 0);
    
    // Reduced acceleration for slower movement
    this.acc = new p5.Vector(random(-0.02, 0.02), random(-0.02, 0.02));
    this.size = random(3, 12); // Slightly larger bubbles for visibility
  }

  move() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
  }

  delete() {
    if (this.pos.x > width + this.size * 2 || this.pos.x < 0 - this.size * 2 || this.pos.y > height + this.size * 2 || this.pos.y < 0 - this.size * 2) {
      let index = bubbles.indexOf(this);
      bubbles.splice(index, 1);
    }
  }

  display() {
    noStroke();
    // Adjust x-coordinate by offsetX to shift the image to the right
    c = self.get(this.pos.x - offsetX, this.pos.y); 
    fill(c);
    ellipse(this.pos.x, this.pos.y, this.size);
  }
}
```