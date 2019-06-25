<template>
  <div class="shutterslider">
    <h1>Animation</h1>
    <div id="container">
      <ul id="banner">
        <li>
          <img src="../assets/dsc-01.jpg" alt="lorempixel.com">
        </li>
        <li>
          <img src="../assets/dsc-02.jpg" alt="lorempixel.com">
        </li>
        <li>
          <img src="../assets/dsc-03.jpg" alt="lorempixel.com">
        </li>
        <li>
          <img src="../assets/dsc-04.jpg" alt="lorempixel.com">
        </li>
        <li>
          <img src="../assets/dsc-05.jpg" alt="lorempixel.com">
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ShutterSlider',
  props: {
    interval: Number
  },
  data () {
    return {
        slideNum: 0
    }
  },
  methods: {
      slice (imageContainer, i, partsAmount, delayTime) {
          let sliceDiv = document.getElementById('slide' + i),
              w = sliceDiv.offsetWidth,
              h = sliceDiv.offsetHeight,
              img = sliceDiv.getElementsByTagName('img')[0].src;

          for (let x = 0; x < partsAmount; x++) {
              let width = x * w / partsAmount + "px";
              let div = document.createElement("div");
              document.getElementById('slide' + i).appendChild(div);
              div.classList.add('slice');
              div.style.left = width;
              div.style.top = 0;
              div.style.width = w / partsAmount + "px";
              div.style.height = h + "px";
              div.style.backgroundImage = "url(" + img + ")";
              div.style.backgroundPosition = "-" + width;
              div.style.backgroundSize = w + "px";
              div.style.transitionDelay = x * delayTime + "s";
          }
      },
      carousel (timeout) {
          let x = this.$data.imageContainers;
          for (let i =  0; i < x.length; i++) {
              x[i].classList.remove("active");
          }
          this.slideNum++;
          if (this.slideNum > x.length) {
              this.slideNum = 1
          }
          x[this.slideNum-1].classList.add("active");
          setTimeout( () => {
              this.carousel(timeout)
          }, timeout);
      }
  },
  mounted() {
      this.$data.imageContainers = document.querySelectorAll('#banner li');
      for ( let i=0; i<this.$data.imageContainers.length; i++ ) {
          this.$data.imageContainers[i].id = 'slide' + i;
      }
      for ( let i = 0; i < this.$data.imageContainers.length; i++ ) {
          this.slice(this.$data.imageContainers[i], i, 10, 0.1);
      }
      this.carousel(this.interval);
  }
}
</script>

<style lang="scss">

body, html {
  padding:0;
  margin:0;
}

#container {
  margin: 5em 0;
}

h1 {
  text-align:center;
  font-family: sans-serif;
}

#banner {
  width:800px;
  margin: 0 auto;
}
ul#banner {
  list-style-type: none;
  position: relative;
  padding: 0;
}

li {
  width: 100%;
  height: 500px;
  position: absolute;
  top: 0;
  left: 0;
}

li img {
  height: auto;
  width: 100%;
  opacity: 0;
}

li .slice {
  position: absolute;
  z-index: 1;
  background-repeat: no-repeat;
  transform: rotateY(-50deg) scale(0.5);
  opacity: 0;
  transform-origin: bottom;
  transition: all 0.6s ease-in-out;
}

li.active .slice {
  opacity: 1;
  transform: rotate(0deg) translateY(0);
}

</style>
