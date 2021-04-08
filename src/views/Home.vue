<template>
  <div class="home">
    <h1 :style="{color: color}">paco</h1>
    <color-picker
      aria-label="color picker"
      @color-change="colorChange"
      :colors="['black', 'red', 'green', 'blue']"
    ></color-picker>
    <bg-color-picker
      aria-label="color picker"
      @backgroundColor-change="backgroundColorChange"
      :colors="['black', 'red', 'green', 'blue']"
    ></bg-color-picker>



    
    <div id="dice">
      <div id="d4-wrap">
        <div id="d4">
          <div class="d4" data-side="1" :style="{backgroundColor: backgroundColor, color: color}">
            <div data-number="2"></div>
            <div data-number="3"></div>
            <div data-number="4"></div>
          </div>
          <div class="d4" data-side="2" :style="{backgroundColor: backgroundColor, color: color}">
            <div data-number="1"></div>
            <div data-number="3"></div>
            <div data-number="4"></div>
          </div>
          <div class="d4" data-side="3" :style="{backgroundColor: backgroundColor, color: color}">
            <div data-number="1"></div>
            <div data-number="2"></div>
            <div data-number="4"></div>
          </div>
          <div class="d4" data-side="4" :style="{backgroundColor: backgroundColor, color: color}">
            <div data-number="1"></div>
            <div data-number="2"></div>
            <div data-number="3"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import ColorPicker from '../components/ColorPicker.vue';
import BgColorPicker from '../components/BgColorPicker.vue';

export default {
  name: 'App',
  components: {
    'color-picker': ColorPicker,
    'bg-color-picker': BgColorPicker,
  },
  data() {
    return {
      color: 'black',
      backgroundColor: 'black',
    };
  },
  methods: {
    colorChange(color) {
      this.color = color;
    },
    backgroundColorChange(backgroundColor) {
      this.backgroundColor = backgroundColor;
    },
  },
}
</script>

<style>
@keyframes tumble { 
  0% { transform: rotateY(0deg) rotateX(0deg) rotateZ(0deg); }
  100% { transform: rotateY(360deg) rotateX(360deg)  rotateZ(360deg); }
}

/* @keyframes spin { 
  0% { transform: perspective(0) rotateZ(0deg) rotateY(0deg); }
  100% { transform: perspective(0) rotateZ(360deg) rotateY(360deg); }
} */
#dice {
  position: absolute;
  top: 50%;
  left: 50%;
  transform-style: preserve-3d;
  animation: spin 10s infinite linear;
  transform: perspective(0);
}
#d4-wrap {
  transform-style: preserve-3d;
  transform: translateX(0) translateZ(0);
}
#d4 {
  transform-style: preserve-3d;
  animation: tumble 8s infinite linear;
}
.d4 {
  --width: 30px;
  --height: 0.8660254;
  --center: 0.288675;
  --offset: calc(var(--center)*var(--center));
  --dihedral-angle: 70.528779deg;
  --co-dihedral: calc(90deg - var(--dihedral-angle));
  --luminance: 50%;
  font-size: 0.5rem;
  width: calc(2 * var(--width));
  height: calc(2 * var(--width) * (var(--height)));
  background-color: hsla(30,100%,var(--luminance),0.4);
  position: absolute;
  clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
  transform-origin: 50% calc(var(--center)*(var(--width)));
  transform-style: preserve-3d;
}

.d4[data-side='1']{
  --luminance: 40%;
  transform: rotateY(120deg) rotateX(var(--co-dihedral))  translateZ(calc(var(--offset)*(var(--width))));
}
.d4[data-side='2']{
  --luminance: 50%;
  transform: rotateX(var(--co-dihedral)) translateZ(calc(var(--offset)*(var(--width))));
}
.d4[data-side='3']{
  --luminance: 60%;
  transform: rotateY(240deg) rotateX(var(--co-dihedral))  translateZ(calc(var(--offset)*(var(--width))));
}
.d4[data-side='4']{
  --luminance: 70%;
  transform:  rotateY(180deg) rotateX(270deg) translateZ(calc((1 + var(--center))*var(--width))) translateY(calc(0px - (var(--height)*(var(--width)))));
}
[data-number]::after {
  position: absolute;
  content: attr(data-number);
  bottom: 0;
  text-align: center;
  left: 0;
  right: 0;
  padding: 0.4rem 0 0.1rem;
  transform-origin: center top;
  transform: rotateX(10deg) rotateY(0deg) rotateZ(0deg);}
.d4[data-side='1'] [data-number='2']::after,
.d4[data-side='2'] [data-number='3']::after,
.d4[data-side='3'] [data-number='1']::after,
.d4[data-side='4'] [data-number='1']::after {
  transform:rotateZ(120deg);
}
.d4[data-side='1'] [data-number='3']::after,
.d4[data-side='2'] [data-number='1']::after,
.d4[data-side='3'] [data-number='2']::after,
.d4[data-side='4'] [data-number='3']::after {
  transform:rotateZ(240deg);
}
</style>