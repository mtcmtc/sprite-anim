# Sprite Animation

Sprite Animations allow you to to implement controllable animations - an accessible alternative to GIF animations

## Get Started

Download the most recent JS and CSS files.

Load JS and CSS files
```html
  <script src="./public/spriteanim.js"></script>
  <link rel="stylesheet" type="text/css" href="./public/spriteanim.css">
```

Setting up the HTML
```html
      <!-- Sprite 1 HTML - options: 8 frames, .8 seconds, autoplay-->

      <div data-sprite="sprite_anim00" data-sprite-src="./assets/test-anim_full.jpg" data-sprite-duration=".8" data-sprite-framecount="8" data-sprite-playback="auto"></div>


      <!-- Sprite 2 HTML - options: 30 frames, 2 seconds, autoplay-->

      <div data-sprite="sprite_anim01" data-sprite-src="./assets/performance-sprites/poloanimation.jpg" data-sprite-duration="2" data-sprite-framecount="30" data-sprite-playback="auto"></div>


      <!-- Sprite 3 HTML - options: 14 frames, 1.5 seconds, hover to play-->

      <div data-sprite="sprite_anim02" data-sprite-src="./assets/linen.jpg" data-sprite-duration="1.5" data-sprite-framecount="14" data-sprite-playback="hover"></div>
```

Instantiate sprite control object
```html
  <script type="text/javascript">
    var sprite_anim_control1 = new wcdAnimControl("sprite_anim00");
    var sprite_anim_control2 = new wcdAnimControl("sprite_anim01");
    var sprite_anim_control3 = new wcdAnimControl("sprite_anim02");
  </script>
```

### CSS

### HTML

### JS
