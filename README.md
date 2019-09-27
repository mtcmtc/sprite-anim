# Sprite Animation

Sprite Animations allow you to to implement controllable animations - an accessible alternative to GIF animations

## Get Started

Download the most recent JS and CSS files.

```html
<style type="text/css">
    
    @keyframes sprite {0% { transform: translateY(0); } 100%{ transform: translateY(-100%); }}
    @-webkit-keyframes sprite {0% { -webkit-transform: translateY(0); } 100%{ -webkit-transform: translateY(-100%);}}
   
    [data-sprite]{position: relative; overflow: hidden;}
    [data-sprite] img{position:absolute;top:0;left:0;width:100%;}
    [data-sprite].anim-loaded img{
      -webkit-animation-name: sprite; animation-name: sprite;
      -webkit-animation-iteration-count: infinite; animation-iteration-count: infinite;
      -webkit-animation-play-state: paused; animation-play-state: paused;}
    [data-sprite].anim-loaded.anim-play img{-webkit-animation-play-state: running;animation-play-state: running;}
  </style>
```

```html
<script type="text/javascript">
    var spriteAnimControl = function(sel){
      this.sprite;
      this.paused = true;

      var that = this;

      this.spriteData = function(sel) {
        thisSprite = document.querySelector('[data-sprite="' + sel + '"]');
        that.sprite = {
          el :  thisSprite,
          filepath : thisSprite.getAttribute('data-sprite-src'),
          frames : thisSprite.getAttribute('data-sprite-framecount'),
          playback : thisSprite.getAttribute('data-sprite-playback'),
          duration : thisSprite.getAttribute('data-sprite-duration'),
          poster : thisSprite.querySelector('img')
        };

        thisSprite.removeAttribute('data-sprite-src');
        thisSprite.removeAttribute('data-sprite-framecount');
        thisSprite.removeAttribute('data-sprite-playback');
        thisSprite.removeAttribute('data-sprite-duration');
      }

      this.loadSprite = function(data, callback) {
        data.img = new Image();
        data.img.onload = callback;
        data.img.src = data.filepath;
      }

      this.calcPAR = function(sprite){
        var w = sprite.img.width;
        var h = sprite.img.height/sprite.frames;
        if(sprite.filepath.indexOf('.svg') > -1){
          /* fix for SVGs in IE11. Use ajax to get SVG as XML */
          jQuery.get(sprite.filepath, function(svgxml){
              /* now with access to the source of the SVG, lookup the values you want... */
              var attrs = svgxml.documentElement.attributes;
              //alert( 'img: ' + attrs.width.value + 'x' + attrs.height.value );
              /* do something with the svg, like add it to the document for example... */
              w = attrs.width.value;
              h = attrs.height.value/sprite.frames;
              sprite.par = ((h/w)*100).toFixed(2);
              sprite.el.style.paddingTop = sprite.par + "%";
          }, "xml");
        }else{
          sprite.par = ((h/w)*100).toFixed(2);
          sprite.el.style.paddingTop = sprite.par + "%";
        }
      }

      this.play = function(){
        that.paused = false;
        if(that.button)that.button.className = "playbutton active";
        that.sprite.el.className += ' ' + 'anim-play';
      }

      this.pause = function(){
        that.paused = true;
        that.sprite.el.classList.remove('anim-play');
        if(that.button)that.button.className = "playbutton";
      }

      this.generatePauseButton = function(){
        var html = "<a class='playbutton'><span class='sds_visually-hidden'>pause play button</span></a>"
        var css = ".sprite_anim-control{position: absolute;bottom:0;padding:1.5%;right:0}.playbutton{cursor:pointer;border-bottom:8px solid transparent;border-left:12px solid #a0968c;border-top:8px solid transparent;display:inline-block;height:0;position:relative;width:0;z-index:1;transition:all 0.2s;-webkit-transition:all 0.2s;-moz-transition:all 0.2s}.playbutton:before{border-radius:0;10 content:'';position:absolute;z-index:2 transition:all 0.2s;-webkit-transition:all 0.2s;-moz-transition:all 0.2s}.playbutton:after{content:'';opacity:0;transition:opacity 0.6s;-webkit-transition:opacity 0.6s;-moz-transition:opacity 0.6s}.playbutton.active{border-color:transparent}.playbutton.active:after{border-left:4px solid #a0968c;border-right:4px solid #a0968c;content:'';height:12px;opacity:1;position:absolute;right:0;top:-7px;width:4px;}",
        style = document.createElement('style');
        div = document.createElement('div');
        
        style.type = 'text/css';
        div.className = 'sprite_anim-control';
        that.sprite.el.appendChild(style);
        that.sprite.el.appendChild(div);
        

        style.innerHTML = css;
        div.innerHTML = html;
        

        that.button = div.lastChild;
        that.button.addEventListener('click', function(){ !that.paused ? that.pause() : that.play();});
      }

      this.constructSprite = function(item){
        that.spriteData(item);

        that.loadSprite(that.sprite, function(e){

          $sprite = that.sprite;

          $sprite.el.classList.add('anim-loaded');
          
          that.calcPAR($sprite);

          var animStyles = "-webkit-animation-timing-function:steps(" + $sprite.frames + ");-webkit-animation-duration:" + $sprite.duration + "s;" + "animation-timing-function:steps(" + $sprite.frames + ");animation-duration:" + $sprite.duration + "s;";
          $sprite.el.appendChild($sprite.img);
          $sprite.el.firstChild.setAttribute("style", animStyles);

          //hide poster image once PAR has been established
          if($sprite.poster != null) $sprite.poster.style.display = "none";

          if($sprite.playback == "hover"){
            $sprite.el.addEventListener('mouseenter', function(){ 
              if(that.paused)that.play();
            });

            $sprite.el.addEventListener('mouseleave', function(){ 
              if(!that.paused)that.pause();
            });
          }else {
            that.generatePauseButton();
            if($sprite.playback == "auto"){that.play();}
          }
        });
      }

      this.init = function(){
        that.constructSprite(sel);
      }

      this.init();
    }
  </script>
```

### CSS

### HTML

### JS
