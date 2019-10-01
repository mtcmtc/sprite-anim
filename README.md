# Sprite Animation

Sprite Animations allow you to to implement controllable animations - an accessible alternative to GIF animations. This method of animation requires assets to be sliced like a [film strip](https://github.com/mtcmtc/sprite-anim/blob/master/assets/ryu-sprite-demo.png?raw=true), allowing CSS3 transforms to translate-y the sprite image like a frame-by-frame animation. (Note: each frame in the image file should be the same height (i.e. a sprite with a height of 300px that has 10 frames should be sliced as a jpeg with 3000px height.)

## Get Started

Download the most recent JS and CSS files or include them in your HTML file.

Load JS and CSS files. Make sure to update the file path.
```html
  <script src="./public/spriteanim.js"></script>
  <link rel="stylesheet" type="text/css" href="./public/spriteanim.css">
```

### Data Attributes

To set up your sprite animation, create a <div> and include the following data attributes:

**data-sprite** – This is essentially an ID attribute used when you instantiate a spriteControl object.

**data-sprite-src** – Add your sprite file path here.

**data-sprite-framecount** – Make sure to include the correct amount of frames. ie, If the [image (example)](https://github.com/mtcmtc/sprite-anim/blob/master/assets/aloe_film.jpg?raw=true) has 14 frames, the sprite-framecount value should be 14.

**data-sprite-duration (optional, default is 3s)** – How long you want the animation to run for in seconds.

**data-sprite-playback (optional, default is paused)**
- auto: adds a pause/play button and autoplays the animation
- hover: no pause/play button but adds hover-to-play.

### Setting up the HTML

```html
      <!-- Sprite 1 HTML - options: 8 frames, .8 seconds, autoplay-->

      <div data-sprite="sprite01" data-sprite-src="./assets/test-anim_full.jpg" data-sprite-duration=".8" data-sprite-framecount="8" data-sprite-playback="auto"></div>


      <!-- Sprite 2 HTML - options: 30 frames, 2 seconds, autoplay-->

      <div data-sprite="sprite02" data-sprite-src="./assets/performance-sprites/poloanimation.jpg" data-sprite-duration="2" data-sprite-framecount="30" data-sprite-playback="auto"></div>


      <!-- Sprite 3 HTML - options: 14 frames, 1.5 seconds, hover to play-->

      <div data-sprite="sprite03" data-sprite-src="./assets/linen.jpg" data-sprite-duration="1.5" data-sprite-framecount="14" data-sprite-playback="hover"></div>
```

### Instantiate sprite control object
```html
  <script type="text/javascript">
    var sprite01 = new spriteControl("sprite01");
    var sprite01 = new spriteControl("sprite02");
    var sprite03 = new spriteControl("sprite03");
  </script>
```
